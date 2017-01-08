## 2.5 Sum List

You have two numbers represented by a linked list, where each node contains a single digit. The digit are stored in reverse order, such that the 1's digit is at the head of the list. Write a function that adds the two numbers and returns the sum as a linked list.

**Example:**

    Input: (7 -> 1 -> 6) + (5 -> 9 -> 2). That is, 617 + 295.
    Output: 2 - > 1 -> 9. That is, 912.

**Follow up:**
Suppose the digits are stored in forward order. Repeat the above problem.

**Ideas:**

It's useful to remember in this problem how exactly addition works. Imagine the problem:

      617
    + 295

First, we add 7 and 7 to get 12. The digit 2 becomes the last digit of the number, and 1 gets carried over to the next step. Second, we add 1, 1, and 9 to get 11. The 1 becomes the second digit, and the other 1 gets carried over the final step. Third and finally, we add 1, 6 and 2 to get 9. So, our value becomes 912.

We can mimic this process recursively by adding node by node, carrying over any "excess" data to the next node. Let's walk through this for the below linked list:

      7 -> 1 -> 6
    + 5 -> 9 -> 2

We do the following:

1. We add 7 and 5 first, getting a result of 12. 2 becomes the first node in our linked list, and we "carry" the 1 to the next sum.

    List: 2 -> ?

2. We then add 1 and 9, as well as the "carry", getting the result of 11. 1 becomes the second element of our linked list, and we carry the 1 to the next sum.

    List: 2 -> 1 -> ?
    
3. Finally, we add 6, 2 and our "carry", to get 9. This becomes the final element of our linked list.

    List: 2 -> 1 -> 9.
    
The code below implements this algorithm:

**Solution:**


    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        return self.addList(l1, l2, 0)
        
    def addList(self, l1, l2, carry):
        if l1 is None and l2 is None and carry == 0:
            return None
        res = ListNode(0)
        sum = carry
        if l1:
            sum += l1.val
        if l2:
            sum += l2.val
        # Second digit of the sum
        res.val = sum % 10
        # Recurse
        if l1 or l2:
        # Be careful to handle the condition when one list is shorted than another, we don't want to get a null pointer exception.
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
            more = self.addList(l1, l2, 1 if sum >= 10 else 0)
            res.next = more
        return res

**Follow-up:**

Part B is conceptually the same(recurse, carry the excess), but has some additional complications when it comes to implementation:

1. One list may be shorter than the other, and we cannot handle this "on the fly". For example, suppose we were adding (1 -> 2 -> 3 -> 4) and (5 -> 6 -> 7). We need to know that the 5 should be matched with the 2, not the 1. We can accomplish this by comparing the lengths of the lists in the beginning and padding the shorter list with zeros.
2. In the first part, successive results were added to the tail (i.e., passed forward). This meant that the recursive call would be passed the carry, and would return the result (which is then appended ti the tail). In this case, however, results are added to the head (i.e., passed backwards). The recursive call must return the result, as before, as well as the carry. This is not terribly challenging to implement, but it is more cumbersome. 
 
We can solve this issue by creating a wrapper class called `PartialSum`, where sum(linked list) exists as SUM.

**Solution to follow-up:**

    class ListNode(object):
        def __init__(self, x):
            self.val = x
            self.next = None

    class PartialSum(object):

        def __init__(self):
            self.SUM = None
            self.carry = 0

    class Solution(object):

        def addTwoNumbers(self, l1, l2):
            """
            :type l1: ListNode
            :type l2: ListNode
            :rtype: ListNode
            """
            len1 = self.getLength(l1)
            len2 = self.getLength(l2)
            # Pad the shorter list with zeros:
            if len1 < len2:
                l1 = self.padList(l1, len2 - len1)
            else:
                l2 = self.padList(l2, len1 - len2)

            # Add Two lists together:
            p_sum = self.partialAddition(l1, l2)

            # If there was a carry value left over, insert this at the front of the list. Otherwise, just return the list
            if p_sum.carry == 0:
                return p_sum.SUM
            else:
                res = ListNode(p_sum.carry)
                res.next = p_sum.SUM
                return res

        def partialAddition(self, l1, l2):
            if l1 is None and l2 is None:
                s = PartialSum()
                return s
            # Add smaller digits recursively.
            s = self.partialAddition(l1.next, l2.next)
            # Add carry to current data:
            val = s.carry + l1.val + l2.val
            # Insert sum of current digits:
            dummy = ListNode(val%10)
            dummy.next = s.SUM
            full_res = dummy
            s.SUM = full_res
            s.carry = val / 10
            return s

        def getLength(self, head):
            if head is None:
                return 0
            return self.getLength(head.next) + 1

        def padList(self, head, n):
            dummy = ListNode(-1)
            new_head = dummy
            for i in xrange(n):
                dummy.next = ListNode(0)
                dummy = dummy.next
            dummy.next = head
            return new_head.next




