## Counting Number of 1 Bits in an Integer

**Guess Version #1: LC191. Number of 1 Bits**

Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the *Hamming weight*).

For example, the 32-bit integer ’11' has binary representation `00000000000000000000000000001011`, so the function should return 3.

**Solution: O(n) time & O(1) Space**

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
            
