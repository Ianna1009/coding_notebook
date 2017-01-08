## List of Depths

Given a binary tree, design an algorithm to create a linked list of all the nodes at each depth. If you have a tree with depth D, you'll have D linked lists.

Example

    Input Tree
           A
          / \
         B   C
        / \   \
       D   E   F


    Output Tree
           A--->NULL
          / \
         B-->C-->NULL
        / \   \
       D-->E-->F-->NULL

Intuition:

Since it's implementing a linked list on each level, so thinking about using level order traversal.

Similar question:

[LeetCode 102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

Instead of putting a dummy after the last node in the current level, we should put a linked list head in the front of the first node.

---
**Solution #1 BFS:**

     class Solution(object):
        def listOfDepth(self, root):
            res = []
            dummy = LinkedTreeNode(0)
            head = LinkedTreeNode(0)
            pre = head
            queue = []
            queue.append(root)
            queue.append(dummy)
            while queue:
                curr = queue.pop(0)
                if curr != dummy:
                    pre.next = curr
                    pre = pre.next
                    if curr.left:
                        queue.append(curr.left)
                    if curr.right:
                        queue.append(curr.right)
                else:
                    pre.next = None
                    res.append(head.next)
                    if not queue:
                        break
                    head.next = queue[0]
                    pre = head
                    queue.append(dummy)
            return res
            
**Soluetion #2: DFS**

    # Definition for binary tree with next pointer.
    # class TreeLinkNode:
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None
    #         self.next = None

    class Solution:
        # @param root, a tree link node
        # @return nothing
        def connect(self, root):
            self.dfs(root, [], 0)

        def dfs(self, root, lists, level):
            if root is None:
                return
            if len(lists) == level:
                l = root
                lists.append(l)
            else:
                l = lists[level]
                l.next = root
                lists[level] = root
            self.dfs(root.left, lists, level+1)
            self.dfs(root.right, lists, level+1)