Given a string:

```python
s = "PAYPALISHIRING"
```

Return its "zigzag pattern":

```python
P   A   H   N
A P L S I I G
Y   I   R
```

```python
s = PAHNAPLSIIGYIR
```

The zig zag pattern must be calculated based on a provided number of rows (`numRows`). For the example above, `numRows == 3`.

## Intuition

At first glance, this question heavily reminds me of [[Spiral Matrix]]. The "trick" to that problem is to figure out what actions we need to repeat in order to simulate a spiral traversal. 

As for zigzags, there's a pattern that repeats regardless of the provided string or the number of rows:

```bash
|    /|    /|    /|
|  /  |  /  |  /  |
|/    |/    |/    |
```

At it's most basic level, a zigzag is a straight line and a diagonal:

```bash
|    /
|  /  
|/    
```

The depth and length of the zigzag can change based on input, but the core pattern remains the same. 

In other words, while we iterate through the characters of the provided string `s`, we can loop downwards until we reach `numRows`, and then iterate diagonally until we reach `0` (utilizing a pointer like `t`).

We can use an auxiliary [[Matrix]] to keep track of the zigzag pattern we create, and then concatenate all rows into one final string. With a bit of math, we can come to the conclusion that the number of columns in the matrix is equal to `math.ceil(len(s) / 2)`:

```python
def convert(self, s: str, numRows: int) -> str:
	# Base case
	if numRows == 1: return s
	
	matrix = [[''] * math.ceil(len(s) / 2) for row in range(numRows)]
	
	t,b,l,r = 0, len(matrix) - 1, 0, len(matrix[0]) - 1
	i = 0
	while i < len(s):
		# Traverse downwards
		while t < b and i < len(s):
			matrix[t][l] = s[i]
			t += 1
			i += 1
		
		# Traverse diagonally
		while t > 0 and l <= r and i < len(s):
			matrix[t][l] = s[i]
			t -= 1
			l += 1
			i += 1
		
	return ''.join(''.join(row) for row in matrix)
```




