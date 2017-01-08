## 198.House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

**Solution: (Naive DP)**

    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        if n <= 1:
            return 0 if n == 0 else nums[0]
        m = [nums[0], max(nums[0], nums[1])]
        for i in xrange(2, n):
            m.append(max(m[i-2] + nums[i], m[i-1]))
        return m[-1]
        
**Solution: (Memorized DP)**

    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        if n <= 1:
            return 0 if n == 0 else nums[0]
        a = 0
        b = 0
        for i in xrange(n):
            tmp = a
            a = b + nums[i]
            b = max(tmp, b)
        return max(a, b)

