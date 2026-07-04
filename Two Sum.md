The most popular DSA question of all time. 

The brute force solution couldn't be more straightforward. Since we know there is exactly **one** answer, we can simply iterate over all numbers and compare any `nums[i]` to any `nums[j]` that equals `target`:

```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
	for i in range(len(nums)):
		for j in range(i, len(nums)):
			if i != j and (nums[i] + nums[j]) == target:
				return [i, j]
```

This question is deceptively simple, but it becomes interesting once we ask the question: Can we solve this with a #TimeComplexity of `O(N)`?

Like many DSA questions, we need to think retroactively - rather than looking for  `x + y = target`, we can instead use some memory to our advantage and look for `x = target - y`

We know what the `target` is the moment we get into the question, so we can use a [[HashMap]] to keep track of seen values and look for the necessary `diff` while iterating:

```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
	seen = {}
	
	for i, n in enumerate(nums):
		diff = target - n
		if diff in seen:
			return [seen[diff], i]
		seen[n] = i
```

**Why a map instead of a set?** Simply because the question asks for the **index** of the two numbers and not the numbers themselves. Since we need to keep track of two related pieces of information at the same time, a map fits in perfectly.