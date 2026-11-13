Simply put, a regular stack that can also return it's minimum element in `O(1)`. This means that **all** functions part of the proposed `MinStack` class must run in `O(1)`

To begin with, we can implement the typical functionality of a Stack:

```python
class MinStack:
	def __init__(self):
		self.stack = []
	
	def push(self, value: int) -> None:
		self.stack.append(value)
	
	def pop(self) -> None:
		self.stack.pop()
	
	def top(self) -> int:
		return self.stack[-1]
```

Python makes this pretty easy, as `pop()` is implemented on Python's `list`. We also know that `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks, so we don't have to worry much about conditionals.

`getMin()` would be trivial if we could just iterate over all numbers in `self.stack`, but we can't. 

Additionally, numbers can enter the stack in any order. We could push `0`, `3`, and `-1`, and if the following input is `"getMin", "pop", "getMin"`, the adequate answer's would be: `-1,` `""`, `0`

What we do have to our advantage is that values are pushed one by one, meaning that at any moment a `value` is pushed, we can compare to whatever minimum we have computed:

```python
class MinStack:
	def __init__(self):
		self.stack = []
		self.minStack = []
	
	def push(self, value: int) -> None:
		self.stack.append(value)
		if self.minStack:
			value = min(value, self.minStack[-1])
		self.minStack.append(value)
	
	def pop(self) -> None:
		self.stack.pop()
		self.minStack.pop()
	
	def top(self) -> int:
		return self.stack[-1]
	
	def getMin(self) -> int:
		return self.minStack[-1]
```

#Drawing this question out is **pivotal** for the understanding of the functionality of the `minStack`. 

Let's go back to the example from earlier:

```python
["MinStack","push(0)","push(3)","push(-1)","getMin","pop","getMin"]
```

Here's how the logic would play out:

1) `MinStack` object is created
2) On the first push, the `stack` and the `minStack` remain identical, there's no previously inserted number, so the minimum **MUST** be whatever we just pushed.
3) `3` is evidently higher than `0`, so the stack gets the actual value appended, but the `minStack` completely ignores it, **re-appending 0 to the top**
4) `-1` is lower than `0`, the `stack` adds it as usual, and `-1` is added to the top of the `minStack`

At this point we would have:

```python
self.stack = [0, 3, -1]
self.minStack = [0, 0, -1]
```

What's important to understand is that due to the order of insertions, 3 could **never** be the minimum value within the `stack`, so `minStack` never has to be aware of its existence.