## 4.8 First Common Ancestor

Design an algorithm and write code to find the first common ancestor of two nodes in a binary tree. Avoid storing additional nodes in a data structure.

**Note: This is not necessarily a binary search tree.**

          _______3______
         /              \
      ___5__          ___1__
     /      \        /      \
     6      _2       0       8
           /  \
           7   4

For example, the lowest common ancestor (LCA) of nodes 5 and 1 is 3. Another example is LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

**Solution #1: (TLE)**

    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        # error check:
        if not self.cover(root, p) or not self.cover(root, q):
            return None
        return self.finder(root, p, q)
    
    def finder(self, root, p, q):
        
        if root is None or p == root or q == root:
            return root
        
        pIsOnLeft = self.cover(root.left, p)
        qIsOnLeft = self.cover(root.left, q)
        if pIsOnLeft != qIsOnLeft:
            return root
        
        childnode = root.left if pIsOnLeft else root.right
        return self.finder(childnode, p, q)
        
    def cover(self, root, p):
        if root is None:
            return False
        if root == p:
            return True
        return self.cover(root.left, p) or self.cover(root.right, p)