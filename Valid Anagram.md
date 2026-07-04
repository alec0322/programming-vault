> Q: Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An **anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

From a mathematical perspective, this means that the frequency of any character `c` in `s` must be equal to the frequency of `c` in `t`
	This implies that if `c` is not in `t`, `s` and `t` could never be anagrams of each other.

Arguably one of the best introductions to [[HashMap]]

If we think in set theory, `s.freq(c) == t.freq(c)`. We can recreate this function using maps.

```python
def isAnagram(self, s: str, t: str) -> bool:
	# Base case
	if len(s) != len(t):
		return False

	s_map, t_map = {}, {}
	
	# Step 1: Fill out maps
	for i in range(len(s)):
		c, d = s[i], t[i]
		s_map[c] = s_map.get(c, 0) + 1
		t_map[d] = t_map.get(d, 0) + 1
	
	# Step 2: Compare maps
	for c in s_map:
		if s_map[c] != t_map.get(c, 0):
			return False
	return True
```

This question also teaches us a nifty trick built into Python dictionaries. We avoid key errors by utilizing the built-in `.get()` function in 2 different ways.

1) In step 1, we use `.get(c, 0)` to populate the map. While iterating through characters, if we hit a char we've not seen yet, `0` acts as a fallback. If we hit a char we've already seen, the function acts as a typical retrieval and gives us the value of `s_map[c]`
   
2) In step 2, we use it to protect ourselves from values that don't exist in `t`. At this point we know for a fact that the 2 strings have the same length, but the maps are not necessarily equal to each other. If iterate over a char that exists in `s` but not in `t`, the result defaults to `0`

Evidently, we don't **need** this function, but the answer is more elegant this way.