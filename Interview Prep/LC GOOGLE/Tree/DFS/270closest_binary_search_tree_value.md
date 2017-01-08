## 270.Closest Binary Search Tree Value

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**

Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.

**Solution:**

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def closestValue(self, root, target):
            """
            :type root: TreeNode
            :type target: float
            :rtype: int
            """
            res = [None]
            self.finder(root, target, res, float('inf'))
            return res[0]

        def finder(self, root, target, res, diff):
            if root is None:
                return 
            tmp = abs(root.val - target)
            if tmp < diff:
                res[0] = root.val
                diff = tmp
            if root.val < target:
                self.finder(root.right, target, res, diff)
            else:
                self.finder(root.left, target, res, diff)