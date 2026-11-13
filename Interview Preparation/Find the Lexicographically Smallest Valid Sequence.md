We are given two strings, `word1` and `word2` 

According to this problem, a string `x` is called **almost equal** to `y` if you can change **at most** one character in `x` to make it identical to `y`

We are also told that a sequence of indices `seq` is "valid" if:
- The indices are sorted in ascending order (i.e. `[0,1,2]`)
- Concatenating the characters at these indices in `word1` in the same order results in a string that is **almost equal** to `word2`

Our goal is to return the lexicographically smallest valid sequence of indices.

## Intuition

This is one of those questions that you have to read more than once to understand, but we can infer a few things from the description:

1) Two strings are almost equal to each other when there is at most a one character difference between them.
2) Any sequence created from `word1` that could possibly be a substring that is almost equal to `word2` has to have the same length as `word2` itself.
3) The indices composing a sequence have to be **ascending**, but not necessarily "next" to each other (meaning that a valid sequence could be `[0,5,7]`)
4) A sequence `a` is **lexicographically smaller** than another sequence `b` if the first element in which the two sequences different is less than the corresponding element in the other. For example, `[0,2,3]` is lexicographically smaller than `[1,2,3]`. Perhaps we can use `sum()` for a quick check? Looks like if `sum(a) < sum(b)`, would give us the same information...

Based on the way the problem is written, we are clearly given a base case on when to check a sequence...

> Concatenating the characters at these indices in `word1` in the same order results in a string that is **almost equal** to `word2`

Based on the inference above, we can say that `len(seq) == len(word2)` is our base case.

It's important to remember that we can change **at most** one character. A word like `aaaaaa` could **never** be "almost equal" to `aaabc`. Perhaps we can use a frequency map to determine if it's even possible to get a sequence in the first place.

Another cheap pass (that would avoid [[Dynamic Programming]]) would be to check if `word2` is in `word1` to begin with, if so we can just return the current location of the substring as a sequence in `O(N)`.

I fail to see the #RecurrenceRelation for the normal case, though. In [[House Robber]], we have a clear decision to make on any recurrence: to either rob the current house or the next one, and if we decide to rob the current house, we cannot possibly rob the house next to it too.

