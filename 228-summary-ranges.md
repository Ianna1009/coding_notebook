## 228. Summary Ranges

Given a sorted integer array without duplicates, return the summary of its ranges.

**For example**, given [0,1,2,4,5,7], return ["0->2","4->5","7"].

**Ideas:**

Intuitively, we can iterate through this given array, by using `left` and `right` to denote the left endpoint of the range and right for the right endpoint. 

* Every time when the number got cut off, we update `left` and `right` with this number.
* Every time when the number is consecutive with precious one, we only update `right` with this number.


**Solution:**

    class Solution(object):
        def summaryRanges(self, nums):
            """
            :type nums: List[int]
            :rtype: List[str]
            """
            res = []
            if not nums:
                return res
            left, right = nums[0], nums[0]
            for i in xrange(1, len(nums)):
                if nums[i] == nums[i-1]+1:
                    right = nums[i]
                else:
                    if left == right:
                        res.append(str(left))
                    else:
                        res.append(str(left) + "->" + str(right))
                    left, right = nums[i], nums[i]
            if left == right:
                res.append(str(left))
            else:
                res.append(str(left) + "->" + str(right))
            return res
            
**Notes(what made it a MEDIUM-DIFFICULTY problem):**

Edge cases:

1. `[0]`
2. `[1, 3]`
3. `[1, 2, 7]`

Also note that we checked two time within and outside of `for` loop, which is unnecessary, we can improve it by:

**Solution #2:**

    class Solution(object):
        def summaryRanges(self, nums):
            """
            :type nums: List[int]
            :rtype: List[str]
            """
            left, n = 0, len(nums)
            res = []
            for right in xrange(n):
                if right + 1 < n and nums[right+1] == nums[right] + 1:
                    right += 1
                    continue
                else: 
                    val = str(nums[left])
                    if right > left:
                        val += "->" + str(nums[right])
                    res.append(val)
                    left = right + 1
            return res
            
**Solution #3:** This referred to "[书影博客](http://bookshadow.com/weblog/2015/06/26/leetcode-summary-ranges/)"

    class Solution(object):
        def summaryRanges(self, nums):
            """
            :type nums: List[int]
            :rtype: List[str]
            """
            left, n = 0, len(nums)
            res = []
            while left < n:
                org_left, val = left, str(nums[left])
                while left + 1 < n and nums[left + 1] - nums[left] == 1:
                    left += 1
                if left > org_left:
                    val += "->" + str(nums[left])
                res.append(val)
                left += 1
            return res
            
                        
            
        
