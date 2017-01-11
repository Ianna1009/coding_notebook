## 213. House Robber II

**Note:** This is an extension of House Robber.

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are **arranged in a circle**. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.


**Solution:**

Based on the MEMO version of House Robber solutions, we can choose either rob the first house or not.

    class Solution(object):
        def rob(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            n = len(nums)
            if n < 2:
                return 0 if n == 0 else nums[0]
            return max(self.robHelper(nums[:-1]), self.robHelper(nums[1:]))
            
        def robHelper(self, nums):
            excl, incl = 0, 0
            for j in xrange(len(nums)):
                i = incl
                e = excl
                incl = e + nums[j]
                excl = max(i, e)
            return max(excl, incl)
        
