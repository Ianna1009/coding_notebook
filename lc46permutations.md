## LC46. Permutations

Given a collection of distinct numbers, return all possible permutations.

For example,

     [1,2,3] have the following permutations:
     
        [
          [1,2,3],
          [1,3,2],
          [2,1,3],
          [2,3,1],
          [3,1,2],
          [3,2,1]
        ]
---

** Solution: **

    class Solution(object):
        def permute(self, nums):
            """
            :type nums: List[int]
            :rtype: List[List[int]]
            """
            ans = []
            self.dfs(nums, ans, [])
            return ans

        def dfs(self, nums, res, tmp):
            if len(nums) == 0:
                res.append([] + tmp)
                return

            for i in xrange(len(nums)):
                tmp.append(nums[i])
                self.dfs(nums[:i] + nums[i+1:], res, tmp)
                tmp.pop()
