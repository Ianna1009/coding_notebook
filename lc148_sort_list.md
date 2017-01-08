## LC148. Sort List


Sort a linked list in O(n log n) time using constant space complexity.

Regardless of space, we can use merge sort in order to achieve O(n log n) time complexity.

**Algorithm**:

    sortList(head)
    1) If head is NULL or there is only one element in the Linked List, then return.
    2) Else divide the linked list into two halves.  
          a, b = split(head); /* a and b are two halves */
    3) Sort the two halves a and b.
          sortList(a);
          sortList(b);
    4) Merge the sorted a and b (using SortedMerge() discussed here) 
       and update the head pointer using head.
         head = merge(a, b);
         
 
 ---
** Solution:** 

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def sortList(self, head):
            """
            :type head: ListNode
            :rtype: ListNode
            """
            if head is None or head.next is None:
                return head
            else:
                head1, head2 = self.split(head)
                left = self.sortList(head1)
                right = self.sortList(head2)
                return self.merge(left, right)

        def split(self, head):
            fast = head.next
            slow = head
            while fast is not None and fast.next is not None:
                fast = fast.next.next
                slow = slow.next
            # slow is in the middle
            head2 = slow.next
            slow.next = None
            return head, head2

        def merge(self, left, right):
            head = TreeNode(0)
            dummy = head
            while left and right:
                if left.val < right.val:
                    dummy.next = left
                    left = left.next
                else:
                    dummy.next = right
                    right = right.next
                dummy = dummy.next
            if left is None:
                dummy.next = right
            if right is None:
                dummy.next = left
            return head.next

