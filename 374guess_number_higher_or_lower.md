## 374.Guess Number Higher or Lower

We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number is higher or lower.

You call a pre-defined API guess(int num) which returns 3 possible results (-1, 1, or 0):

    -1 : My number is lower
     1 : My number is higher
     0 : Congrats! You got it!

**Example:**

    n = 10, I pick 6.
    Return 6.
    
**Solution: **

    # The guess API is already defined for you.
    # @param num, your guess
    # @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
    # def guess(num):

    class Solution(object):
        def guessNumber(self, n):
            """
            :type n: int
            :rtype: int
            """
            start = 1
            end = n
            while start + 1 < end:
                mid = (start + end) / 2
                g = guess(mid)
                if g == -1:
                    end = mid - 1
                elif g == 1:
                    start = mid + 1
                else:
                    return mid
            return end if guess(start) == 1 else start
