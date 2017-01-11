## Counting Number of 1 Bits in an Integer

### Guess Version #1: LC191. Number of 1 Bits

Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the *Hamming weight*).

For example, the 32-bit integer ’11' has binary representation `00000000000000000000000000001011`, so the function should return 3.

**Solution #1: O(n) time & O(1) Space**

    class Solution(object):
        def hammingWeight(self, n):
            """
            :type n: int
            :rtype: int
            """
            cont = 0
            for i in bin(n):
                if i == '1':
                    cont += 1
            return cont
            
**Solution #2: n & (n-1) trick: O(n) time & O(1) Space**

    class Solution(object):
        def hammingWeight(self, n):
            """
            :type n: int
            :rtype: int
            """
            cont = 0
            for i in bin(n):
                if i == '1':
                    cont += 1
            return cont
            
### Guess Version #2: LC338. Counting Bits

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

**Example:**

For num = 5 you should return [0,1,1,2,1,2].

**Follow up:**

* It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
* Space complexity should be O(n).
* Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

**Hint:**

1. You should make use of what you have produced already.
2. Divide the numbers in ranges like [2-3], [4-7], [8-15] and so on. And try to generate new range from previous.
3. Or does the odd/even status of the number help you in calculating the number of 1s?
   
**Solution:**

     class Solution(object):
        def countBits(self, num):
            """
            :type num: int
            :rtype: List[int]
            """
            if num < 2:
                return [0, 1] if num == 1 else [0]
            total = [0, 1]
            for i in xrange(2, num+1):
                if i % 2 == 0:
                    total.append(total[i/2])
                else:
                    total.append(total[i/2] + 1)
            return total
                         
            
