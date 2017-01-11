## Maximum Sum with Constrians

**Guess Version #1 Non-Negative: (House Robber)**
 
Given an array of non-negative integers, determine the maximum sum of a subsequence with the constraint that no 2 numbers in the sequence should be adjacent in the array. 
 
**Ideas:**

This is a classic dynamic programming problem. At the last state, either plus the last number or not, i.e. take max(dp[i-1], dp[i-2]+array[i])

**Solution:** 

    class Solution(object):
        def rob(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            n = len(nums)
            if n < 1:
                return 0
            res = 0
            dp = [0] * (n+1)
            dp[1] = nums[0]
            for i in xrange(1, n):
                dp[i+1] = max(dp[i-1]+nums[i], dp[i])
            return dp[-1]
            
**Solution with Memorization:**


