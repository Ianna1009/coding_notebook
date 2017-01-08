## LC80.Remove Duplicates from Sorted Array 2


Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

    For example,
    Given sorted array nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.

---
** Solution: **

    class Solution(object):
        def removeDuplicates(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            n = len(nums)
            if n < 3:
                return n
            i, count = 0, 1
            for j in xrange(1, n):
                if nums[j] != nums[i]:
                    i += 1
                    count = 1
                    nums[i] = nums[j]
                else:
                    if count < 2:
                        i += 1
                        nums[i] = nums[j]
                    count += 1
            return i+1