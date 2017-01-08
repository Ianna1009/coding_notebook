## 4.10 Check Subtree

Given two binary trees, check if the first tree is subtree of the second one. A subtree of a tree T is a tree S consisting of a node in T and all of its descendants in T. The subtree corresponding to the root node is the entire tree; the subtree corresponding to any other node is called a proper subtree.

For example, in the following case, tree S is a subtree of tree T.

        Tree 2
          10  
        /    \ 
      4       6
       \
        30


        Tree 1
              26
            /   \
          10     3
        /    \     \
      4       6      3
       \
        30

**Solution:** 

Traverse the tree T in **preorder** fashion. For every visited node in the traversal, see if the subtree rooted with this node is identical to S.

    def checkSubtree(self, t1, t2):
        # Base Case, empty tree is the subtree of any tree
        if t2 is None:
            return True
        return self.checker(t1, t2)
        
    def checker(self, t1, t2):
        if t1 is None:
            return False
        elif t1.val == t2.val and self.match(t1, t2):
            return True
        return self.checker(t1.left, t2) or self.checker(t1.right, t2)
    
    def match(self, t1, t2):
        if t1 is None and t2 is None:
            return True
        if t1 is None or t2 is None:
            return False
        if t1.val != t2.val:
            return False
        return self.match(t1.left, t2.left) and self.match(t1.right, t2.right)
        
        
   
        
