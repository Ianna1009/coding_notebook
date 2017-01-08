## Remove 0 sum subtree

Question:

Given a binary tree, remove its subtrees whose sum is zero.

---

** Solution: **

    class TreeNode(object):

        def __init__(self, x):
            self.val = x
            self.left = None
            self.right = None

    class Solution(object):

        def remove0Subtree(self, root):
            newRoot, sum = self.dfs(root)
            return newRoot, sum

        def dfs(self, root):
            if root is None:
                return
            if root.left is None and root.right is None:
                return root, root.val
            root.left, leftSum= self.dfs(root.left)
            root.right, rightSum = self.dfs(root.right)
            tmp = leftSum + rightSum + root.val
            if tmp == 0:
                return None, tmp
            return root, tmp

