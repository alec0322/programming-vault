Given an array:
```python
nums = [1,2,3]
```

Return all of its **permutations**. In the context of this question, the definition of all permutations is the same as the one used in statistics: all possible rearrangements of all the elements in the array.

Not to be confused by all possible [[Combinations]]. In a combination, the order of elements doesn't affect combination count. Let's say we wanted to select 2 elements from the `nums` array above.

### Possible combinations

```python
[1, 2]
[1, 3]
[2, 3]
```

### Possible permutations

```python
[1, 2]
[2, 1]
[1, 3]
[3, 1]
[2, 3]
[3, 2]
```

Notice that `[1, 2]` and `[2, 1]` count as separate permutations but **not** as separate combinations.

Using this logic, we can think of all combinations as all unique sets we can create from a collection of elements. Likewise, we can think of all permutations as all unique tuples we can create from said collection.

## Intuition

We can use a [[Depth First Search]] algorithm, passing originally an empty array alongside a set of "available" elements. On each call of the DFS, we can check what numbers are still available and recurse:

![[Permutations Sketch|1000]]

Our base case would of course be returning whenever the passed array has a length equal to the original `nums` array, where we would also append to an external `response` array:

```python
def permute(self, nums: List[int]) -> List[List[int]]:
	res = []
	
	def dfs(curr, available):
		if len(curr) == len(nums):
			res.append(curr[:]) # append a shallow copy of curr
			return
		else:
			i = 0
			while i < len(available):
				n = available.pop(i)
				curr.append(n)
				dfs(curr, available)
				curr.pop()
				available.insert(i, n)
				i += 1				
	
	dfs([], nums[:]) # pass a shallow copy of nums to leave input untouched
	
	return res
```

What makes this a backtracking problem is the idea that we mutate the `curr` and `available` objects, recurse, and **return them to their original state**