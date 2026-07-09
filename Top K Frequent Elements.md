Exactly as the title describes, we must return the top `K` frequent elements within an array.

This is one of those that is extremely easy to visualize:

```python
nums = [1,1,1,2,2,3]
k = 2
```

With the input above, the answer would be `[1,2]` (or `[2,1]`, as the order in which we return the elements doesn't matter).

This question should remind us of [[Valid Anagram]], as the concept of **frequency** is very tightly knit to [[HashMap]]'s (at least within the LeetCode world)

We can use a frequency map to simultaneously keep track of seen numbers and their respective frequencies within `nums`, and then return the top `K` elements using sorting functions.

```python
def topKFrequent(self, nums: List[int], k: int) -> List[int]:
	freq = {}
	for n in nums:
		freq[n] = freq.get(n, 0) + 1
	
	# Persist unsorted tuples
	tuples = list(freq.items())
	
	# Sort tuples by x[1], the frequency, in reverse order
	tuples.sort(key=lambda x: x[1], reverse=True)
	
	# Return top K elements
	return [tuples[i][0] for i in range(k)]
```

The trick is to use the built-in `items()` function of Python Dictionaries. Running:

```python
freq = {1:3, 2:1, 1:1}
print(list(freq.items())) # Returns [(1,3), (2,1), (1,1)]
```

The sorting function is what's truly doing the heavy lifting in this answer.
1) They `key` parameter tells the sorting function what logic to use when sorting, in this case we tell it to sort by the value of `x[1]` (which is equivalent to the 2nd value of any `x` variable passed)
2) The `reverse` boolean is obvious, not necessary but makes our lives easier as we are looking for the top `k` (highest to smallest) elements - Sorting is from smallest to highest by default.