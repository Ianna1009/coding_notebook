## Missing Ranges

Given a sorted integer array where the range of elements are in the inclusive range [lower, upper], return its missing ranges.

**For example,** 

    given [0, 1, 3, 50, 75], lower = 0 and upper = 99, 
    return ["2", "4->49", "51->74", "76->99"].


**Solution:**

    class Solution(object):
        def findMissingRanges(self, nums, lower, upper):
            """
            :type nums: List[int]
            :type lower: int
            :type upper: int
            :rtype: List[str]
            """
            res = []
            # initialize prev as lower-1
            prev = lower - 1
            curr = 0
            for i in xrange(len(nums)+1):
                if i == len(nums):
                    curr = upper + 1
                else:
                    curr = nums[i]
                if curr - prev > 1:
                    if prev + 1 == curr - 1:
                        res.append(str(prev+1))
                    else:
                        res.append(str(prev+1) + "->" + str(curr-1))
                prev = curr
            return res
        
        