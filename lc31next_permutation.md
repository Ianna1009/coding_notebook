## LC31.Next Permutation

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

**Here are some examples.** Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

      1,2,3 → 1,3,2
      3,2,1 → 1,2,3
      1,1,5 → 1,5,1
---
**Solution:**


    class Solution(object):
        def nextPermutation(self, nums):
            """
            :type nums: List[int]
            :rtype: void Do not return anything, modify nums in-place instead.
            """
            if len(nums) < 2:
                return
            k = self.increasePos(nums)
            if k == len(nums)-1:
                nums[k], nums[k-1] = nums[k-1], nums[k]
            elif k == 0:
                nums.reverse()
            else:
                nums[k:] = sorted(nums[k:])
                s = self.findNext(nums[k-1], nums[k:])
                nums[k+s], nums[k-1] = nums[k-1], nums[k+s]


        def increasePos(self, nums):
            i = len(nums)-1
            while i >= 0 and nums[i] <= nums[i-1]:
                i -= 1
            return i

        def findNext(self, x, arr):
            # arr is sorted already
            i = 0
            while i < len(arr) and x >= arr[i]:
                i += 1
            return i 
