We are given a `houses` array representing a row of houses in a neighborhood. `houses[i]` represents how much money is inside of house `i`. We need to come up with a path that will give us not only the most money, but also will not get us caught.

```python
houses = [1,2,3,1]
```

Why not just maximize the amount of money we get out of this heist and rob all houses in the neighborhood? Well, there's a security system that will catch us **if we rob two houses that are next to each other**.
## Brute Force

We can use a DFS to visit all possible paths we can take and then return the maximum profit.

Evidently, this is a terrible solution, if there are 1 million houses next to each other, we could have a #TimeComplexity of `O(2^1000000)`

```python
def rob(self, nums: List[int]) -> int:
	
	def dfs(i):
		if i >= len(nums):
			return 0
		else:
			return max(dfs(i + i), nums[i] + dfs(i + 2))
	
	return dfs(0)
```

## DP (Top-Down)

We can use [[Memoization]] to cache results as we rob houses.

```python
def rob(self, nums: List[int]) -> int:
	memo = [-1] * len(nums)
	
	def dfs(i):
		if i >= len(nums):
			return 0
		elif memo[i] != -1:
			return memo[i]
		else:
			memo[i] = max(dfs(i + i), nums[i] + dfs(i + 2))
			return memo[i]
	
	return dfs(0)
```