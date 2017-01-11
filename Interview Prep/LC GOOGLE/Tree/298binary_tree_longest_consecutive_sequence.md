## 298. Binary Tree Longest Consecutive Sequence

Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

**For example,**

       1
        \
         3
        / \
       2   4
            \
             5
  Longest consecutive sequence path is 3-4-5, so return 3.
    
    
       2
        \
         3
        / 
       2    
      / 
     1
Longest consecutive sequence path is 2-3,not 3-2-1, so return 2.


**Ideas:**

* Traverse from root to leaf, whenever touch the bottom return to the previous level.
* While traversing if child node value is the next consecutive integer, tmp_count += 1. Otherwise, res = max(res, tmp_count), tmp_count = 1.
* Note that minimum res should be 1 since only one leaf is also itself a sequence.

**Solution:**

    def longestConsecutive(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        res = [0]
        ## Be careful: prev of root in -inf, and count initialized to be 1
        self.trav(root, -float('inf'), res, 1)
        return res[0]
    
    def trav(self, root, prev, res, tmp_count):
        if root is None:
            return 
        if root.val == prev+1:
            tmp_count += 1
        ## Be careful: if not consecutive any more, tmp_count should be reset
        else:
            tmp_count = 1
        res[0] = max(res[0], tmp_count)
        prev = root.val
        self.trav(root.left, prev, res, tmp_count)
        self.trav(root.right, prev, res, tmp_count)
        