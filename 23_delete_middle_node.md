## 2.3 Delete Middle Node

Implement an algorithm to delete a node in the middle (i.e. any node but the first and last node, not necessarily the exact middle) of a singly linked list, given only access to that node.

**Example:**

    Input: the node c from the linked list a -> b -> c -> d -> e -> f
    Result: nothing is returned, but the new linked list looks like a -> b -> d -> e -> f
    
**Ideas:**

* Since head is not given only the node is given, so we can simple access to that node, and copy the next node value to this one, and delete the next node.

**Solution:**

    def deleteNode(self, node):
        # Cannot delete anything from the list:
        if node is None or node.next is None:
            return False
        node.val = node.next.val
        node.next = node.next.next
        return True

**Note**

Note that this problem cannot be solved if the node to be deleted is the last node in the linked list.


