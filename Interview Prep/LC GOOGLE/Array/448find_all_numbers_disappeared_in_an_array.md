## 448.Find All Numbers Disappeared in an Array

Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Similar Problem: [442. Find All Duplicates in an Array](https://ianna1009.gitbooks.io/leectcode-solution/content/442find_all_duplicates_in_an_array.html)

**Example:**

    Input:
    [4,3,2,7,8,2,3,1]

    Output:
    [5,6]
    
**Solution: **

    def findDisappearedNumbers(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        n = len(nums)
        for i in xrange(n):
            ind = abs(nums[i])-1
            if nums[ind] > 0:
                nums[ind] *= -1
        return [i+1 for i in xrange(n) if nums[i] > 0 ]
        

**Cleaner Solution:**

    class Solution(object):
        def findDisappearedNumbers(self, nums):
            """
            :type nums: List[int]
            :rtype: List[int]
            """
            # For each number i in nums,
            # we mark the number that i points as negative.
            # Then we filter the list, get all the indexes
            # who points to a positive number
            for i in range(len(nums)):
                index = abs(nums[i]) - 1
                nums[index] = - abs(nums[index])
    
            return [i + 1 for i in range(len(nums)) if nums[i] > 0]        
            
refer to [discussion](https://discuss.leetcode.com/topic/68838/python-4-lines-with-short-explanation)
    
