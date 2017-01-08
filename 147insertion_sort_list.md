## 147.Insertion Sort List

Sort a linked list using insertion sort.

---
**Solution #1: Use `next`**

      # Definition for singly-linked list.
      # class ListNode(object):
      #     def __init__(self, x):
      #         self.val = x
      #         self.next = None

      class Solution(object):
          def insertionSortList(self, head):
              """
              :type head: ListNode
              :rtype: ListNode
              """
              if head is None:
                  return head
              dummy = ListNode(0)
              while head:
                  tmp = dummy
                  next = head.next
                  while tmp.next and tmp.next.val < head.val:
                      tmp = tmp.next

                  head.next = tmp.next
                  tmp.next = head
                  head = next

              return dummy.next
              
              
**Solution #2: Use `prev`**

    class Solution(object):
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummy = ListNode(-float('inf'))
        while head:
            tmp = dummy
            prev = dummy
            next = head.next
            while tmp != None and tmp.val < head.val:
                prev = tmp
                tmp = tmp.next
                
            head.next = tmp
            prev.next = head
            head = next
            
        return dummy.next


