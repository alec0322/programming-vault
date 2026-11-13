The most basic example of [[HashSet]] usage.

The entire basis of a set is that it's items are unique, we can check if a collection of items has a duplicate if the length of the set of its items is **not** equal to the length of the provided array.

```python
def containsDuplicate(self, nums: List[int]) -> bool:
	return len(set(nums)) != len(nums)
```

This will have a time AND space complexity of `O(N)`.

This MAY look like a `T = O(1)` solution, but its important to note that inserting EACH item into our set will still take `N` iterations, it just happens behind the scenes inside of `set(nums)`

There's an even better solution:

```python
def containsDuplicate(self, nums):
    seen = set()
    for n in nums:
        if n in seen:
            return True
        seen.add(n)
    return False
```

Starting out with an empty set and iterating through each item manually **could** potentially save both time and space.

With an array like:
```python
nums = [1,1,2,3]
```

Our final set would contain only 1 item:
```python
seen = {1}
```

And we would've iterated just **2 times**.

Whereas in the previous algorithm we would've been forced to iterate through N items and create a set of size N.