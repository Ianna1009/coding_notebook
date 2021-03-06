## 276.Paint_Fence

There is a fence with n posts, each post can be painted with one of the k colors.

You have to paint all the posts such that no more than two adjacent fence posts have the same color.

Return the total number of ways you can paint the fence.

**Note:**
n and k are non-negative integers.

**Solution:**

    def numWays(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: int
        """
        if n < 2:
            return k if n == 1 else 0
        a = k
        b = k*k
        for i in xrange(2, n):
            b, a = (k-1)*(b+a), b
        return b
        
Details see from: [https://ianna1009.gitbooks.io/leectcode-solution/content/276paint_fence.html](https://ianna1009.gitbooks.io/leectcode-solution/content/276paint_fence.html)
        