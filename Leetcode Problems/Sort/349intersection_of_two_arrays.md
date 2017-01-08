## 349.Intersection of Two Arrays

Given two arrays, write a function to compute their intersection.

    Example:
    Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].

**Note:**
Each element in the result must be unique.
The result can be in any order.

**tags: **Binary Search, Hash Table, Two Pointers, Sort

**Ideas:**
1. Binary Search: array must be sorted. => Two arrays, which one to sort or both?
2. Once sorted, Two pointers must be slower than binary search.
3. Maybe sort the longer array, then do binary search for each element in the shorter array in the sorted array in O(min(n lg m, m lg n)).

    class Solution(object):
        def intersection(self, nums1, nums2):
            """
            :type nums1: List[int]
            :type nums2: List[int]
            :rtype: List[int]
            """
            m, n = len(nums1), len(nums2)
            
            ## nums1 always be the longer one
            if m < n:
                nums1, nums2 = nums2, nums1
            nums1.sort()
            
            res = []
            for item in nums2:
                start, end = 0, len(nums1)-1
                while start <= end:
                    mid = start + (end - start) / 2
                    if item > nums1[mid]:
                        start = mid + 1
                    elif item < nums1[mid]:
                        end = mid - 1
                    else:
                        if item not in res:
                            res.append(item)
                        break
            return res
            
            
            
     

