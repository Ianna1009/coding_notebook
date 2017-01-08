## 4.6 Inorder Successor in BST

Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

Note: If the given node has no in-order successor in the tree, return null.

**Ideas:**
1. If p has right child, then the leftmost right child will be its successor.
2. Elif p has no right child, then using in-order traversal, its successor is its leftmost parent node. As we are using root, therefore we will look for node p while we are only:
    1. changing parent node every time we search for the left sub-tree,
    2. not changing parent node every time we search for the right sub-tree.

**Solution #1 (Using Root)**

    def inorderSuccessor(self, root, p):
        """
        :type root: TreeNode
        :type p: TreeNode
        :rtype: TreeNode
        """
        if p.right:
            while p.left:
                p = p.left
            return p
        else:
            return self.firstParent(root, None, p)
    
    def firstParent(self, root, parent, p):
        if root is None:
            return None
        if root.val > p.val:
            return self.firstParent(root.left, root, p)
        if root.val < p.val:
            return self.firstParent(root.right, parent, p)
        return parent

**Solution #2 (Using Parent)**
    
    
