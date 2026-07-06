Thanks to [[Valid Anagram]], we determined that it's fairly simple to check if two strings are anagrams of each other. But what if we had `n` many strings that **could** be anagrams of each other? What if we wanted to group them together if they were?

- Checking if any string `s` is an anagram of any string `t` will take `O(K)`, where `K` is the length of the strings.
- Comparing all strings against each other within an array of `strs` will take `O(N^2)`

This would leave us with a theoretical double for-loop where we check for anagrams every time -`O(N^2 * K)` is evidently highly inefficient.

[[Hashing]] tells us that computers like to assign "keys" to values it has to remember. We can apply this concept to this question, assigning "keys" to strings based on their character combinations.

```python
from collections import defaultdict

def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
	res = defaultdict(list)
	
	for s in strs:
		key = [0] * 26
		for c in s:
			key[ord(c) - ord('a')] += 1
		res[tuple(key)].append(s)
	
	return list(res.values())
```

I love this question not just because the solution feels super elegant, but also because its one that really enforces your brain to think like a machine.

Like many other good LeetCode questions, it teaches us some nice tricks:
- `defaultdict(list)` creates a #dict in which any new key has an empty array assigned by default. This allows us to blindly `append` strings onto a newly created `key`. If the key already exists in the dictionary, then we have no issues, if it doesn't, `defaultdict` protects us.
- `tuple(key)` makes the entire `key` into a non-mutable, unique type.
- `ord(c)` gives us the [[ASCII]] value of `c`.