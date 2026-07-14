A **Binary Search Tree** is a certain kind of tree that is defined by the following:
- The left subtree of a node contains only nodes with keys **strictly less than** the node's key.
- The right subtree of a node contains only nodes with keys **strictly greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

For any given node `n`, `n.left.val < n.val` and `n.right.val > n.val`. Take the following example:

![[Binary Search Tree Example]]

At first glance, the `6` looks out of place, how can `5`'s child be `9` but then `9`'s child be `6`? Regardless of how the tree is formed, **every node to the right of `5` is strictly greater than `5`**, this means the tree is a valid BST.

Visually its easy to tell whether a BST is valid or not, but how can we translate this onto an algorithm? The key is to realize that the [[In-Order Traversal]] of a BST **MUST** output a non-decreasing list of numbers. The in-order traversal of the tree above would look as follows:

![[In Order Traversal Example]]

```python
in_order = [1,5,6,9,11]
```

In fact, this is where in-order gets its name. Evidently the traversal can be applied to any tree, but when applied to a BST, the nodes are visited **in order**.

We can then use this traversal to determine whether a tree is a valid BST:

```python
def isValidBST(self, root: Optional[TreeNode]) -> bool:
	isValid = True
	stack = []
	
	def inOrder(node):
		nonlocal isValid
		if not node:
			return
		else:
			inOrder(node.left)
			if stack and stack[-1] >= node.val:
				isValid = False
			stack.append(node.val)
			inOrder(node.right)
	
	inOrder(root)
	
	return isValid
```

