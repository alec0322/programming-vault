The concept is simple: When looking at a tree from top to bottom, what's the maximum distance between the root and a leaf node?

Like most Tree algorithms, the solution can be approached using a [[Depth First Search]] algorithm or a [[Breadth First Search]] algorithm.

It's important to understand the difference between the [[Depth (Trees)]] and the [[Height (Trees)]] of a tree.
- The #Depth refers to the distance of a node from the root (`root` is `0`)
- The #Height refers to the distance of a node from the deepest leaf node.
## DFS

We can traverse through all the existing paths of a tree using recursion, getting the `max` value of any two paths until all paths are visited and compared.

```python
def maxDepth(self, root: Optional[TreeNode]) -> int:
	if not root:
		return 0
	else:
		return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```

## BFS

I would consider the BFS solution to be more inefficient here, as we require a queue to keep track of all nodes within the tree. This would take up `O(N)` in memory in the worst case:

```python
def maxDepth(self, root: Optional[TreeNode]) -> int:
	if not root:
		return 0

	queue = deque([root])
	depth = 0
		
	while queue:
		depth += 1
		for i in range(len(queue)):
			node = queue.popleft()
			if node.left:
				queue.append(node.left)
			if node.right:
				queue.append(node.right)
	
	return depth
```