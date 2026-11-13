Alice and Bob play a game with piles of stones. The objective is to get more rocks than your opponent, where at each turn the player can take a pile from either end of the row (`piles[0] or piles[len(piles)-1]`)

![[Stone Game Sketch]]

Some more rules apply:
- The number of piles is even (`len(piles) % 2 == 0`)
- The total number of stones across the row is odd (`sum(piles) % 2 != 0`)
- Alice and Bob take turns one after the other
- The player with the most stones once all piles are taken (`len(piles) == 0`) wins

## Intuition

Right off the bat, this question seems to be a carbon copy of [[Predict the Winner]], which makes me think this is problem involves both [[Dynamic Programming]] and [[Game Theory]]

Going off a typical DP approach, the #RecurrenceRelation would be the decision a player has at any one turn: **pick either the first pile of stones or the last**. Any turn in the game requires for this decision to be made.

There is one important distinction though. The introduction tells us that we can assume "Alice and Bob play optimally", but playing optimally is NOT the same thing as picking the `max(piles[0], piles[len(piles)-1])`. Take the following example:

```python
piles = [1,2,5,2]
```

If we defined playing optimally as getting the max value of either end of the row, then the game would go as follows:

```python
# Turn 1
piles = [1,2,5,2] # Alice picks the last pile, her score 2

# Turn 2
piles = [1,2,5] # Bob picks the last pile, his score 5

# Turn 3
piles = [1,2] # Alice picks the last pile, her score 4

# Turn 4
piles = [1] # Only 1 pile left, Bob picks it and his score is 6
```

If Alice were to truly play optimally, however, she could win the game. If she picked the first pile on the first turn, the pile with most stones (`piles[2]`) would remain blocked until the third turn, allowing her to win the game.

It's also important to note that Bob will also play optimally, so finding any path were Alice wins is also incorrect.

```python
def stoneGame(self, piles: List[int]) -> bool:
	def dfs(choices, turn, p1, p2):
		if len(choices) == 0:
			# Game ended, check if Alice won this game
			return p1 >= p2
		else:
			if turn % 2 == 0:
				# Alice plays
				pick_first = dfs(
					choices[1:],
					turn + 1,
					p1 + choices[0],
					p2
				)
				pick_last = dfs(
					choices[:len(choices)-1],
					turn + 1,
					p1 + choices[len(choices)-1],
					p2
				)
				return pick_first or pick_last
			else:
				# Bob plays
				pick_first = dfs(
					choices[1:],
					turn + 1,
					p1,
					p2 + choices[0]
				)
				pick_last = dfs(
					choices[:len(choices)-1],
					turn + 1,
					p1,
					p2 + choices[len(choices)-1]
				)
				return pick_first and pick_last
	
	return dfs(piles, 0, 0, 0)
```

The trick here is to understand the Game Theory behind the DFS written. If Alice picks **either** the first pile **or** the last pile, and Bob were to theoretically pick both (where one of the two choices would be the most optimal) could Alice still win?


---


Although the solution above works, there's a more optimal way to write the DFS. Since we are determining whether Alice can win, we can treat the game a bit differently: if Bob scores, Alice loses points. This idea makes the #RecurrenceRelation a bit easier to write.

It's useful to think of some DP algorithms as a hybrid between a loop and a DFS (refer to [[House Robber]]). Since we know that at any turn either player has at most two moves, we can write the recurrence relation using [[Two Pointers]], where `l` represents the first pile and `r` represents the last.

```python
def stoneGame(self, piles: List[int]) -> bool:
	@lru_cache(None)
	def dp(turn, l, r):
		if l > r: return 0
		if turn % 2 == 0:
			# Alice plays
			pick_first = piles[l] + dp(turn + 1, l + 1, r)
			pick_last = piles[r] + dp(turn + 1, l, r - 1)
			return max(pick_first, pick_last)
		else:
			# Bob plays
			pick_first = -piles[l] + dp(turn + 1, l + 1, r)
			pick_last = -piles[r] + dp(turn + 1, l, r - 1)
			return min(pick_first, pick_last)
	
	return dp(0, 0, len(piles)-1) > 0
```

The funniest thing about this problem, however, is that since the number of piles is ALWAYS even, and Alice ALWAYS plays first, she can always win this game (since she's assumed to play optimally)