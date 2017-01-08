## LC297.Serialize and Deserialize Binary Tree

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

For example, you may serialize the following tree


      1
     / \
    2   3
       / \
      4   5

as "[1,2,3,null,null,4,5]", just the same as how LeetCode OJ serializes a binary tree. 

You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

---
** Solution_1:(PreOrder Traversal) **

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Codec:

        def serialize(self, root):
            """Encodes a tree to a single string.

            :type root: TreeNode
            :rtype: str
            """
            res = []
            def pretrav(node):
                if node:
                    res.append(str(node.val))
                    pretrav(node.left)
                    pretrav(node.right)
                else:
                    res.append("#")
            pretrav(root)
            return " ".join(res)

        def deserialize(self, data):
            """Decodes your encoded data to tree.

            :type data: str
            :rtype: TreeNode
            """
            def doit():
                val = next(vals)
                if val == '#':
                    return None
                node = TreeNode(int(val))
                node.left = doit()
                node.right = doit()
                return node
            vals = iter(data.split())
            return doit()

---
**Solution_2:(Level-Order Traversal)**

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Codec:

        def serialize(self, root):
            """Encodes a tree to a single string.

            :type root: TreeNode
            :rtype: str
            """
            if root is None:
                return '[]'
            res = [root.val]
            q = []
            q.append(root)
            while q:
                node = q.pop(0)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
                res.append(node.left.val if node.left else "null")
                res.append(node.right.val if node.right else "null")
            while res and res[-1] == "null":
                res.pop()
            return '[' + ','.join(map(str, res)) + ']'


        def deserialize(self, data):
            """Decodes your encoded data to tree.

            :type data: str
            :rtype: TreeNode
            """
            if data == "[]":
                return None
            nodes = [[TreeNode(x), None][x == 'null'] for x in data[1:-1].split(',')]
            q = []
            q.append(nodes.pop(0))
            root = q[0]
            while q:
                parent = q.pop(0)
                leftChild = nodes.pop(0) if nodes else None
                rightChild = nodes.pop(0) if nodes else None
                parent.left, parent.right = leftChild, rightChild
                if leftChild:
                    q.append(leftChild)
                if rightChild:
                    q.append(rightChild)
            return root
