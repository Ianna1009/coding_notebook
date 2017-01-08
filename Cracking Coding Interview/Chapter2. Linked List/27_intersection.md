## 2.7 Intersection

Given two (singly) linked lists, determine if the two lists intersect. Return the intersecting node. Note that the intersection is defined based on reference, not value. That is, if the kth node of the first linked list is the exact same node (by referenced) as the jth node of the second linked list, then they are intersecting.

**Ideas:**

1. Determine if there's an intersection.
    *  One approach would be to use a hashtable and just throw all the linked list nodes into there. We would need to be careful to reference the linked list by their memory location, not by their value.
    *  An easier way is just to traverse to the end of each of linked list and compare the last node. (Given the fact that there's no cycle)
      
2. Finding the intersecting node.
    If we know the lengths of two linked lists, then the difference between those two linked list will tell us how much to chop off.
    
3. Steps:
    * Run through each linked list to get the lengths and the tails.
    * Compare the tails.
    * Set two pointers to the start of each linked list.
    * On the longer linked list, advance its pointer by the difference in lengths.
    * Now, traverse on each linked list until the pointers are the same.

**Solution:**
    
    def findIntersection(self, l1, l2):
        if l1 is None or l2 is None:
            return None
        # Get lengths and tails:
        res1 = self.getTailAndSize(l1)
        res2 = self.getTailAndSize(l2)
        
        # If different tails, return no intersection
        if res1[0] != res2[0]:
            return False
            
        # Set Pointers to the start pof each linked list.
        shorter = l1 if res1[1] < res2[1] else l2
        longer = l2 if res1[1] < res2[1] else l2
        
        # Chop off the starting of longer linked list if they are at diff lengths
        longer = self.getKthNode(longer, abs(res1[1] - res2[1])
        
        # Move both pointers until you have a collision
        while shorter != longer:
            shorter = shorter.next
            longer = longer.next
        return shorter
        
    def getTailAndSize(self, head):
        if head is None:
            return (None, 0)
        size = 0
        while head.next:
            size += 1
            head = head.next
        return (head, size+1)
    
    def getKthNode(self, head, k):
        while k > 0 or head:
            head = head.next
            k -= 1
        return head
        
        