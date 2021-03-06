## Maximum Sum with Constrians

**Guess Version #1 Non-Negative: (House Robber)**
 
Given an array of non-negative integers, determine the maximum sum of a subsequence with the constraint that no 2 numbers in the sequence should be adjacent in the array. 
 
**Ideas:**

This is a classic dynamic programming problem. At the last state, either plus the last number or not, i.e. take max(dp[i-1], dp[i-2]+array[i])

**Solution: O(n) time, O(n) Space** 

    class Solution(object):
        def rob(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            n = len(nums)
            if n < 1:
                return 0
            dp = [0] * (n+1)
            dp[1] = nums[0]
            for i in xrange(1, n):
                dp[i+1] = max(dp[i-1]+nums[i], dp[i])
            return dp[-1]
            
**Solution with Memorization: O(n) time, O(1) Space**

    class Solution(object):
        def rob(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            n = len(nums)
            if n == 0:
                return 0
            # excl is the sum of not including number i, incl is the sum of including number i 
            excl, incl = 0, 0
            for i in xrange(n):
                in, ex = incl, excl
                incl = ex + nums[i]
                excl = max(in, ex)
            return max(excl, incl)
            
**Guess Version #2 With Negative Integers**

    class Solution(object):
        def rob(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            n = len(nums)
            if n == 0:
                return 0
            isAllNegative = True
            allNegativeMax = -float('inf')
            # excl is the sum of not including number i, incl is the sum of including number i 
            excl, incl = 0, 0
            for i in xrange(n):
                if nums[i] >= 0:
                    isAllNegative = False
                    in, ex = incl, excl
                    incl = ex + nums[i]
                    excl = max(in, ex)
                else:
                    excl = incl
                    if isAllNegative and nums[i] > allNegativeMax:
                        allNegativeMax = nums[i]
                    
            return max(excl, incl) if not isAllNegative else allNegativeMax
            
            






