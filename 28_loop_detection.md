## 2.8 Loop Detection

Given a circular linked list, implement an algorithm that returns the node at the beginning of the loop.

**Definition:**

Circular linked list: A(corrupt) linked list in which a node's next pointer points to an earlier node, so as to make a loop in the linked list.

**Part 1: Detect if the list has a loop**

Using `fastRunner + slowRunner` technique. They must eventually meet.

**Part 2: When do they collide?**

Let's assume that the linked list has a "non-looped" part of size k.

1. We know that for every p steps SlowRunner takes, FastRunner has taken 2p steps. Therefore when SlowRunner enters the looped portion after k steps, FastRunner has taken 2k steps total and must be 2k-k = k steps into the looped portion. Since k might be much larger than the loop length, we should actually write this as mod(k, loo_size) steps, which we well denote as K.

2. if FastRunner is loop_size steps behind SlowRunner, and FastRunner catches up at a rate of 1 step per unit of time, then they must meet after loop_size steps. **At this point, they will be k steps before the head of the loop. Let's call this Let's call this point CollisionSpot**.

**Part 3: How to find the start of the loop?**

We now know that CollisionSpot is k nodes before the start of the loop. Because K = mode(k, loop_size) (or k = k + M * loop_size), it is also correct to say that it is k nodes from the loop start. For example, if node N is 2 nodes into a 5 node loop, it is also correct to say that it is 7, 12, or even 397 nodes into the loop.

Therefore, both CollisionSpot and LinkedListHead are k nodes from the start of the loop. Now if we move the fastRunner to LinkedListHead, they will each be k nodes from LoopStart. Moving them at the same speed will cause them to collide again at the start of the loop.

---
**Impementation Steps:**

1. Create two pointers, Fast and slow
2. Move Fast at a rate of 2 steps and slow at a rate of 1 step.
3. When they collide, move Fast to LinkedListHead. Keep slow where it is.
4. Move Slow and fast at a rate of one step. Return the new collision point.

**Solution:**

    def findBeginning(self, head):
        slow = head
        fast = head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            if slow == fast:
                break
        # No cycle check:
        if fast is None or fast.next is None:
            return None
        # Move fast to head, keep slow where it is
        fast = head
        while slow != fast:
            slow = slow.next
            fast = fast.next
        return slow

