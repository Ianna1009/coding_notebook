## 2.1 Remove Duplicates

Write code to remove duplicates from an unsorted linked list?

**Follow-up:**
How would you solve this problem if a temporary buffer is not allowed?

**Solution #1 (Using a Hash Set):**

      def deleteDups(self, head):
          """
          nType: linkedlist Node
          """
          hashset = set()
          prev = None
          while head:
              if head.val is hashset:
                  prev.next = head.next
              else:
                  hashset.add(head.val)
                  prev = head
              head = head.next    

The above takes O(N) time, where N is the number of elements in the linked list.

**Follow-Up:**
**Solution #2 (Using Two Pointers):**

If we don't have a buffer, we can iterate with two pointers: `curr` which iterates through the linked list and `runner` which checks all subsequent nodes for duplicates.

    def deleteDups(self, head):
        curr = head
        while curr:
            runner = curr
            while runner.next:
                if runner.next.val == curr.val:
                    runner.next = runner.next.next
                else:
                    runner = runner.next
            curr = curr.next
This code runs in O(1) space, but O(N^2) time.
