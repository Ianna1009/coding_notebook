## 257.Binary Tree Paths

Given a binary tree, return all root-to-leaf paths.

**For example**

   given the following binary tree:

       1
     /   \
    2     3
     \
      5
      
   All root-to-leaf paths are:

    ["1->2->5", "1->3"]
    
**Solution:**

    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution:
        # @param {TreeNode} root
        # @return {string[]}
        def binaryTreePaths(self, root):
            res = []
            self.helper(root, res, [])
            return ["->".join(x) for x in res]

        def helper(self, root, res, tmp):
            if root is None:
                return
            if root.left is None and root.right is None:
                res.append(tmp+[str(root.val)])
                return
            self.helper(root.left, res, tmp+[str(root.val)])
            self.helper(root.right, res, tmp+[str(root.val)])