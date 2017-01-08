## BST Print As Sorted Array

Binary Search Tree每个node都是int, 要return一个所有node的sorted array. 用DFS/recursion做，O(N)时间O(N)空间。N是树里节点的个数。

** Solution: (Recursive) ** 

解法同binary tree的inorder traversal：

    class Solution(object):
        def inorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            if root is None:
                return []
            else:
                return self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right)


** Solution: (Iterative): **

    class Solution(object):
        def inorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            res = []
            s = []
            if root is None:
                return res

            while root != None or s:
                if root != None:
                    s.append(root)
                    root = root.left
                else:
                    tmp = s.pop()
                    res.append(tmp.val)
                    root = tmp.right
            return res
