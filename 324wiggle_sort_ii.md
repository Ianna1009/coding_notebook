## 324. Wiggle Sort II

Given an unsorted array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....

**Example:**
(1) Given nums = [1, 5, 1, 1, 6, 4], one possible answer is [1, 4, 1, 5, 1, 6]. 
(2) Given nums = [1, 3, 2, 2, 3, 1], one possible answer is [2, 3, 1, 3, 1, 2].

**Note:**
You may assume all input has valid answer.

**Follow Up:**
Can you do it in O(n) time and/or in-place with O(1) extra space?

**Discuss:**
1. The difference here is '>' and '<' w/o. '=', which means you have to make duplicates nonconsecutive, in `Wiggle Sort I`, duplicates can be exists in the result like:  [1,1,1,5,4,6], while here it's no longer correct.
2. O(n) time sort: Bucket Sort
3. O(1) in-place sort: Quick Sort, insertion sort


---
**Solution #1: Naive Sort (219 ms)**

**O(n lg n) in time, O(n) in space:**

    class Solution(object):
        def wiggleSort(self, nums):
            """
            :type nums: List[int]
            :rtype: void Do not return anything, modify nums in-place instead.
            """
            size = len(nums)
            snums = sorted(nums)
            for x in range(1, size, 2) + range(0, size, 2):
                nums[x] = snums.pop()
                
 
**Solution #2: Quick Sort **

Based on the first solution:
1. Instead of sorting the whole array ( no need to completely sort), we only need to find position where the whole array is split into two halves, i.e. **find the median of the array**. This way, time complexity will decrease to O(n).
2. Considering the arrangement method from solution 1, we can also get even indices and odd indices using the same method.
3. Last step, instead of using auxiliary array, we can just put numbers that are larger than median in the odd positions, and smaller ones in the even positions.

**Algorithm:**

