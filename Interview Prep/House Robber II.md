Almost the exact same problem as [[House Robber]], with the only difference being that `houses[0]` is next to `houses[len(houses) - 1]` 

The trick to [[House Robber]] in the first place is realizing that we will ONLY get caught if we rob two houses that are next to each other. Take:

```python
houses = [1,1,1,1000000,1,1]
```

Visually, one might say: "Why would I rob anything but `houses[3]`? It's value is a million times bigger than all other houses?" 
	The key is to remember that our goal is to **maximize** - If we rob `houses[1]`, `houses[3]`, and `houses[5]` we can walk out with $1,000,002 instead of "just" $1,000,000.

In other words, no matter how much more money one house has than another, the largest number will **always** come from alternating between houses. The same logic applies to this problem, the only difference is that if we rob `houses[0]`, we **cannot** rob `houses[n - 1]`

Take an array like:

```python
houses = [1,3,5,2]
```

Virtually, we only have 2 paths to take as a robber: rob either `house[0]` through `house[n-1]`, or `house[1]` through `house[n]` 

![[House Robber II Sketch]]

Even if we add another house, the idea remains the same:

```python
houses = [1,3,5,2,6]
```

![[House Robber II Sketch 2]]

Of course, the [[House Robber]] logic still applies for either the red path or the blue path:
- If we decide to rob `houses[0]`, we have to pick either `houses[2]` OR `houses[3]` (`0` through `n-1`)
- Likewise, If we decide to rob `houses[1]`, we have to pick either `houses[3]` OR `houses[4]` (`1` through `n`)

This would be our #RecurrenceRelation

## DP (Top-Down)

```python
def rob(self, nums: List[int]) -> int:
	if len(nums) == 1:
		return nums[0]
	
	path1_memo = [-1] * len(nums)
	path2_memo = [-1] * len(nums)
	
	def path1(i):
		if i >= len(nums) - 1:
			return 0
		elif path1_memo[i] != -1:
			return path1_memo[i]
		else:
			path1_memo[i] = max(path1(i + 1), nums[i] + path1(i + 2))
			return path1_memo[i]
	
	def path2(i):
		if i >= len(nums):
			return 0
		elif path2_memo[i] != -1:
			return path2_memo[i]
		else:
			path2_memo[i] = max(path2(i + 1), nums[i] + path2(i + 2))
			return path2_memo[i]
	
	return max(path1(0), path2(1))
```

Although not the prettiest solution, I came up with this one without looking at any code references whatsoever.
	The idea is that we utilize different [[Depth First Search]] algorithms for Path 1 (`0` through `n-1`) or Path 2 (`1` through `n`)