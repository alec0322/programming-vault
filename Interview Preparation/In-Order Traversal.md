When the in-order traversal algorithm is applied to a BST, the nodes are output **in order**.

![[In Order Traversal Example]]

## Recursive Approach

We can use a helper function to perform the traversal itself while we externally track results within a `res` array.

```python
def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
	res = []
	
	def inOrder(node):
		if not node:
			return
		else:
			inOrder(node.left)
			res.append(node.val)
			inOrder(node.right)
	
	inOrder(root)
	return res
```

