## Note

Some notes need to remember:  

1. Add values to some key in dict.\(set default if this key not in dict\)

    i. Method 1: Using `dict.setdefault(key, default = None)`

            >>> d = {}
            >>> for k, v in s:
            ...     d.setdefault(k, []).append(v)
            ...
            >>> d.items()
            [('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]
    ii. Method 2: Using `collections`, which will be **much faster** than the above one:

            >>> s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
            >>> d = defaultdict(list)
            >>> for k, v in s:
            ...     d[k].append(v)
            ...
            >>> d.items()
            [('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]
    ---

2. x &gt;&gt; 1: divide by 2  
   x &lt;&lt; 1: multiply by 2.

3. Reverse a Linked List:

   ```
    def getReverse(self, head):
        new_head = None
        while head:
            dummy = ListNode(head.val)
            dummy.next = new_head
            new_head = dummy
            head = head.next
        return new_head
   ```

4. n & (n-1): drops the lowest set bit.

        For example: n = 00101100
        1) n = 00101100, then n-1 = 00101011, so n & (n-1) = 00101000. Count = 1
        2) n = 00101000, then n-1 = 00100111, so n & (n-1) = 00100000. Count = 2
        3) n = 00100000, then n-1 = 00011111, so n & (n-1) = 00000000. Count = 3

    This way, we can count 1s in a number
    
    
