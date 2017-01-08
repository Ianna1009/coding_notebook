## 2.2 Return Kth to Last

Implement an algorithm to find the kth to last element of a singly linked list.

**Ideas:**

* Think about solving it using both iteratively and recursively.
* Remember that Recursive solutions are often clear but less optimal. For example, in this problem, the recursive implementation is about half the length of the iterative solution but also takes O(n) space, where n is the number of elements in the linked list.

**Solution #1 (Using Recursion):**

This algorithm recurses through the linked list. When it hits the end, the method passes back a counter set to 0. Each parent call adds 1 to this counter. When the counter equals to k, we know that we've reached the kth to last element of the linked list.

    def printKthToLast(self, head, k):
        if head is None:
            return (1, head)
        idx, node = self.printKthToLast(head.next, k)
        if idx == k:
            return (idx, node)
        return (idx+1, head)
        
        
**Solution #2 (Using Iteration):**

    def printKthToLast(self, head, k):
        if head is None:
            return None
        fast = head
        for i in xrange(len(k)):
            if fast:
                fast = fast.next
            else:
                return None
        slow = head
        while head:
            fast = fast.next
            slow = slow.next
        return slow
        
        

