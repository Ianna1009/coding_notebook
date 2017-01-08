## 2.6 Palindrome

Implement a function to check if a linked list is a palindrome.

**Example:**

0 -> 1 -> 2 -> 1 -> 0.

**Solution #1: Reverse and Compare**
Reverse the while linked list and compare the reversed list to the original list. If they are the same, the lists are palindrome.

    def isPalindrome(self, head):
        reversed = self.getReverse(head)
        return self.isSame(reversed, head)
      
    def getReverse(self, head):
        new_head = None
        while head:
            dummy = ListNode(head.val)
            dummy.next = new_head
            new_head = dummy
            head = head.next
        return new_head
    
    def isSame(self, l1, l2):
        while l1 and l2:
            if l1.val != l2.val:
                return False
            l1 = l1.next
            l2 = l2.next
        return l1 == None and l2 == None
        
**Noticed that for a palindrome, only half list needs to be checked**

---

**Solution #2: Iterative Approach**

1. Push the first half into a stack
2. Every time pop one from the stack and compare it to the second half.

        def isPalindrome(self, head):
            fast, slow = head, head
            stack = []
            while fast and fast.next:
                stack.append(slow.val)
                fast = fast.next.next
                slow = slow.next
            
            # Odd number of elements, we skip the middle element:
            if fast:
                slow = slow.next
            while slow:
                if stack.pop() != slow.val:
                    return False
                slow = slow.next
            return True
**Notice that you have to skip the middle element when the number is odd!!!!**

---

**Solution #3: Recursive Approach**


            


        
    
        
        
      