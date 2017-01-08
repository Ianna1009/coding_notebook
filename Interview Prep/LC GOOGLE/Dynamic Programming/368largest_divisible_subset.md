## 368.Largest Divisible Subset

Given a set of distinct positive integers, find the largest subset such that every pair (Si, Sj) of elements in this subset satisfies: `Si % Sj = 0 or Sj % Si = 0`.

If there are multiple solutions, return any subset is fine.

**Example 1:**

    nums: [1,2,3]

    Result: [1,2] (of course, [1,3] will also be ok)
**Example 2:**

    nums: [1,2,4,8]

    Result: [1,2,4,8]
    
**Ideas:**

1. Constrains of adding elements are:  `Si % Sj = 0 or Sj % Si = 0`
2. For one current element, to determine if there are any integers to add afterwards we need to iterate the rest of `nums`. Based on the constrains in #1 we may have several options to move forwards.
3. Choices + Constrains = Backtracking? Obviously there exists some repeats, we may try backtracking first to see if it'll TLE.

**Solution #1 (TLE): **

    def largestDivisibleSubset(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = []
        MAX = [0]
        self.helper(nums, res, [], MAX)
        return res[-1] if len(res) > 0 else res
        
    def helper(self, nums, res, tmp, MAX):
        if len(nums) == 0:
            if len(tmp) > MAX[0]:
                res.append([]+tmp)
                MAX[0] = len(tmp)
            return
        for i in xrange(len(nums)):
            curr = nums[i]
            validNums = self.getValidNums(nums[i+1:], curr)
            self.helper(validNums, res, tmp+[curr], MAX)
            
    def getValidNums(self, nums, x):
        return [y for y in nums if y % x == 0 or x % y == 0]
        
**Analysis:**

It turns out this solution got a TLE. But we can use the same idea with a memorization. Maybe it's better.

**Solution #2 (With Memorization):**

    def largestDivisibleSubset(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = []
        MAX = [0]
        nums.sort()
        memo = collections.defaultdict(int)
        self.helper(nums, res, [], MAX, memo)
        return res[-1] if len(res) > 0 else res
        
    def helper(self, nums, res, tmp, MAX, memo):
        if len(nums) == 0:
            if len(tmp) > MAX[0]:
                res.append([]+tmp)
                MAX[0] = len(tmp)
            return
        for i in xrange(len(nums)):
            curr = nums[i]
            if memo[curr] <= len(tmp):
                memo[curr] = len(tmp)
                validNums = self.getValidNums(nums[i+1:], curr)
                self.helper(validNums, res, tmp+[curr], MAX, memo)
            
    def getValidNums(self, nums, x):
        return [y for y in nums if y % x == 0]
        

The DP method refers to: [http://bookshadow.com/weblog/2016/06/27/leetcode-largest-divisible-subset/](http://bookshadow.com/weblog/2016/06/27/leetcode-largest-divisible-subset/)

**Solution #3 (DP):**

    def largestDivisibleSubset(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if nums == []:
            return []
        nums = sorted(nums)
        size = len(nums)
        dp = [1] * size
        pre = [None] * size
        for x in range(size):
            for y in range(x):
                if nums[x] % nums[y] == 0 and dp[y] + 1 > dp[x]:
                    dp[x] = dp[y] + 1
                    pre[x] = y
        idx = dp.index(max(dp))
        ans = []
        while idx is not None:
            ans += nums[idx],
            idx = pre[idx]
        return ans
                
                
        

                
                
        
                
                
        

