The go-to [[Stack]] LeetCode question.

A string composed of parentheses can only be valid if every open parenthesis has an equivalent closed parenthesis of the **same kind**.

Take the following string:
```python
s = "(){}[]"
```

`s` is considered "valid" as each open parenthesis has a corresponding closed parenthesis.

A corresponding counterpart is not the only requirement. Take `t`, for example:

```python
t = "(({)}[])"
```

`t` has a corresponding closed parenthesis for each open parenthesis.
	Yet, the nested `{` is accompanied by a `)`, rather than a `}`, meaning this string is invalid. This is because open parentheses must be closed in the correct order by characters of the same type. This requirement negates the possibility of using a simple frequency map.


If we use a stack to track the position of parentheses, any time we encounter a closed parenthesis `c` within the string, we know there **must** be a corresponding open parenthesis `d` at the top of our stack for the string to be valid.

Additionally, since we know exactly what the denominated "open" and "closed" parentheses are, we can use a [[HashMap]] to programmatically fetch these relationships in `O(1)`
	To a human, a closed parenthesis would evidently be `)`, but programmatically we could make it whatever character we want, like `%`. 
 
```python
def isValid(self, s: str) -> bool: 
	closedToOpen = {'}': '{', ')': '(', ']': '['}
	stack = []
	
	for c in s:
		if c in closedToOpen:
			if stack and closedToOpen[c] == stack[-1]:
				stack.pop()
			else:
				return False
		else:
			stack.append(c)
	
	return not stack
```

