## 4.5 Valid BST

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

**Example 1:**

        2
       / \
      1   3
    Binary tree [2,1,3], return true.
    
**Example 2:**

        1
       / \
      2   3
    Binary tree [1,2,3], return false.
    
**Solution #1: In-Order Traversal**

Using In-Order Traversal, we'll eventually get a sorted array. Otherwise it's not valid.

    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        res = self.inTrav(root)
        i = 0
        while i < len(res)-1:
            if res[i] >= res[i+1]:
                return False
            i += 1
        return True

    def inTrav(self, root):
        if root is None:
            return []
        else:
            return self.inTrav(root.left) + [root.val] + self.inTrav(root.right)

**Solution #2: The MIN/MAX Solution**

    def isValidBST(self, root):
        return self.checkBST(root, None, None)

    def checkBST(self, root, MIN, MAX):
        if root is None:
            return True
        if (MIN != None and root.val <= MIN) or (MAX != None and root.val >= MAX):
            return False
        if not self.checkBST(root.left, MIN, root.val) or not self.checkBST(root.right, root.val, MAX):
            return False
        return True