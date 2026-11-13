Before even starting the question, it's important to define a **Binary Tree**:

> [!NOTE] [geeks](https://www.geeksforgeeks.org/dsa/binary-tree-data-structure/#google_vignette)
> A **Binary Tree Data Structure** is a hierarchical data structure in which each node has at most two children, referred to as the left child and the right child.

It's helpful to think of [[Recursion]] when solving tree-related LC questions. A **lot** of tree algorithms (or at least many of the mainstream ones) use recursion to some extent.

## Depth First Search

Since we only ever have to worry about two nodes at a time, the inversion of a Binary Tree couldn't be more simple: for any `TreeNode`, assign any existing `left` node to `right` and vice versa.

```python
def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
	if not root:
		return
	else:
		root.right, root.left = root.left, root.right
		self.invertTree(root.left)
		self.invertTree(root.right)
		return root
	
```
