## LeetCode101. Symmetric Tree

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, 

this binary tree [1,2,2,3,4,4,3] is symmetric:

        1
       / \
      2   2
     / \ / \
    3  4 4  3

But the following [1,2,2,null,3,null,3] is not:
       
        1
       / \
      2   2
       \   \
       3    3
       
Bonus points if you could solve it both **recursively and iteratively.**

---
**Recursive:**
1. basic case: 空节点，返回True
2. 非空节点：左子树和右子树比较：
    1. 两节点val相等
    2. 左节点的左子树和右节点的右子树对称
    3. 左节点的右子树和右节点的左子树对称
 
** Solution:(39 ms) **

    class Solution(object):
        def isSymmetric(self, root):
            """
            :type root: TreeNode
            :rtype: bool
            """
            if root is None:
                return True
            else:
                return self.dfs(root.left, root.right)

        def dfs(self, left, right):
            if left is None or right is None:
                return right == left
            if left.val != right.val:
                return False
            return self.dfs(left.left, right.right) and self.dfs(left.right, right.left)


---
** Iteration: **
1. 遍历整个树，左子节点和右子节点需要相等或都为空
2. 左子节点的左子节点和右子结点的右子结点需要相等或都为空；
3. 左子节点的右子结点和右子结点的左子节点需要相等或都为空；
4. 需要注意的问题：子节点是否为空

**Solution: **
