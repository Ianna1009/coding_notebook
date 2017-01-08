## 70.Climbing Stairs

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Solution: **

    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        a = 1
        b = 1
        for i in xrange(2, n+1):
            tmp = a
            a = b
            b += tmp 
        return b
        
  