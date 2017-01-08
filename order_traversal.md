## Order_Traversal

Before Interview, In-order traversal, pre-order traversal and post-order traversal should be mastered very well!

**LeetCode 94. Binary Tree In-order Traversal**

Basic implementation is like:

    def inorderTraversal(root):
        if root != None:
            inorderTraversal(root.left)
            visit(root)
            inorderTraversal(root.right)
            
**LeetCode 144. Binary Tree Preorder Traversal

Basic implementation is similar:

    def preorderTraversal(root):
        if root != None:
            visit(root)
            preorderTraversal(root.left)
            preorderTraversal(root.right)
            
           
** LeetCode 145. Binary Tree Postorder Traversal


        

