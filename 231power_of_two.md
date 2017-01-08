## 231. Power of Two

Given an integer, write a function to determine if it is a power of two.

**Solution #1: (Bit Manipulation) **

    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        # O(1) in time
        return n > 0 and (not (n & (n-1)))
        
**Solution #2: (Recursion)**
        
    def isPowerOfTwo(self, n):
    
        # O(lgn) in time, similar as using iteration
        if n == 0:
            return False
        if n == 1:
            return True
        if n % 2 == 1:
            return False
        else:
            return self.isPowerOfTwo(n/2)
            
**Solution #3: (Math)**

    def isPowerOfTwo(self, n):
    
        # Make use of the range of an integer = -2147483648 (-2^31) ~ 2147483647 (2^31-1), the max possible power of two = 2^30 = 1073741824. O(1) in time.

        return n>0 and (1073741824 % n == 0)
