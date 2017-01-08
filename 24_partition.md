## 2.4 Partition

Write code to partition a linked list around a value x, such that all nodes less than x come before all nodes greater than or equal to x. If x is contained within the list, the values of x only need to be after the elements less than x (see below). The partition element x can appear anywhere in the "right partition"; it does not need to appear between the left and right partitions.

**Example:**

Input: 3 -> 5 -> 8 -> 5 -> 10 -> 2 -> 1 [partition = 5]
Output: 3 -> 1 -> 2 -> 10 -> 5 -> 5 -> 8

**Ideas:**

* If this were an array, we would need to be careful about how we shifted elements. Array shifts are very expensive.
* In a linked list, the situation is much easier. Rather than shifting and swapping elements, we can actually create two different linked lists: one for elements less than x, and one for elements greater than or equal to x.
* We iterate through the linked list, inserting elements into our before list to our after list. Once we reach the end of the linked list and have completed this splitting, we merge the two lists.

**Solution #1 (More Stable):**

    def partition(self, head, x):
        beforeStart = linkedNode(0)
        afterStart = linkedNode(0)
        beforeEnd = beforeStart
        afterEnd = afterStart
        while head:
            if head.val < x:
                # Insert head into end of before list:
                beforeEnd.next = head
                beforeEnd = head
            else:
                afterEnd.next = head
                afterEnd = head
            # Need to break link between head and head.next:
            next = head.next
            head.next = None
            head = next
        if beforeStart is None:
            return afterStart.next
        #Merge before list and after list:
        beforeEnd.next = afterStart.next
        return beforeStart.next
        
**Solution #2 (A shorter One):**

If it's annoying using four different variables for tracking two linked lists. We can make it a  bit shorter.

If we don't care about making the elements of the list "stable" (which there's no obligation to, since the interviewer hasn't specified that), then we can instead rearrange the elements by growing the list at the head and tail.

In this approach, we start a "new" list (using the existing nodes). Elements bigger than the pivot element are put at the tail and elements smaller are put at the head. Each time we insert an element, we update either the head or tail.

    def partition(self, head, x):
        dummy = head
        tail = head
        
        while head:
            if head.val < x:
                # insert current node(head) at the beginning:
                head.next = dummy
                dummy = head
            else:
                # insert current node at tail:
                tail.next = head
                tail = head
            head = head.next
        # Don't forget to make tail.next = None to end this linked list
        tail.next = None
        return dummy
        
        

            