## Check Balanced Tree

Check if a binary tree is balanced or not. Definition of a balanced tree is that its heights of the two subtrees never differ by more than one.

---

**Solution_1 Recursive:**

We can implement a solution based on the definition. We can simply recurse through the entire tree, and for each node, compute the heights of each subtree.

    def isBalanced(self, root):
        if root is None:
            return True # Base case
        heightDiff = self.getHeight(root.left) - self.getHeight(root.right)
        if abs(heightDiff) > 1:
            return False
        else:
            return self.isBalanced(root.left) and self.isBalanced(root.right)
            
    def getHeight(self, root):
        if root is None:
            return -1
        else:
            return max(self.getHeight(root.left), self.getHeight(root.right)) + 1
            
** Solution_2:**


    class Solution(object):
        def isBalanced(self, root):
            """
            :type root: TreeNode
            :rtype: bool
            """
            return self.dfs(root) != -float('inf')

        def dfs(self, root):
            if root is None:
                return 0
            left = self.dfs(root.left)
            right = self.dfs(root.right)
            if abs(left - right) > 1:
                return -float('inf')
            return max(left, right) + 1