## 400.Nth Digit

Find the nth digit of the infinite integer sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...

**Note:**
n is positive and will fit within the range of a 32-bit signed integer (n < 231).

**Example 1:**

    Input:
    3

    Output:
    3
**Example 2:**

    Input:
    11

    Output:
    0

    Explanation:
    The 11th digit of the sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... is a 0, which is part of the number 10.
    
**Solution: **

    def findNthDigit(self, n):
        """
        :type n: int
        :rtype: int
        """
        start = 1
        cont = 9
        length = 1
        while n > cont*length:
            n -= cont*length
            cont *= 10
            length += 1
            start *= 10
        start += (n-1) / length
        t = str(start)
        return ord(t[(n - 1) % length]) - ord('0')