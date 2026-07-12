Synonymous with the [[Binary Tree Level Order Traversal]] LC question, the BFS algorithm is one of the most popular tree traversal algorithms.

The easiest way to picture what a BFS does is with a few drawings. Take a binary tree like the following:

![[Binary Tree Example]]

A BFS would let us iterate over the nodes in the following order: `1A, 2A, 2B, 3A, 3B`. Effectively from top to bottom, from left to right, one level at a time.

![[Level Order Traversal]]

BFS algorithms are also synonymous with [[Queues]], as each level is formed from the nodes that were appended to the queue during the processing of the previous level. Since a tree always starts at one node, the first level is always the root of the tree:

```python
def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
	queue = deque([root])
	level_order = []
	
	while queue:
		level = []
		for i in range(len(queue)):
			node = queue.popleft()
			if node:
				level.append(node.val)
				queue.append(node.left)
				queue.append(node.right)
		if level:
			level_order.append(level)
	
	return level_order	
```
