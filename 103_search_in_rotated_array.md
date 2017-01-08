## 10.3/LC33. Search in Rotated Array

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

---
**Solution:**

    class Solution(object):
        def search(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: int
            """
            if nums is None:
                return -1

            start = 0
            end = len(nums)-1

            while start+1 < end:
            # 注意这里的循环条件是start+1 < end, 如果是start<end，会出现tle, 因为可能有一支会出现空集，导致start ＝ mid这种赋值没有意义，死循环！！
                mid = (end+start)/2
                if nums[mid] == target:
                    return mid
                # 如果左支有序：
                if nums[start] < nums[mid]:
                    # 如果target在左支中间，则选择左支，end = mid
                    if nums[start] <= target and target <= nums[mid]:
                        end = mid
                    # 如果target不在左支中，则需要选择右支，start＝mid
                    else:
                        start = mid
                 # 如果左支无序，先讨论右支，类似的分析：
                else:
                    if nums[mid] <= target and target <= nums[end]:
                        start = mid
                    else:
                        end = mid
            # 最后终止的时候若没有返回结果(mid不是想要的值)，则有可能start或者end就是想要的值：
            if nums[start] == target:
                return start
            elif nums[end] == target:
                return end

            return -1
            
            
 **Improved Solution:**
 
We can search an element in one pass of Binary Search. The idea is to search

    1) Find middle point mid = (l + h)/2
    2) If key is present at middle point, return mid.
    3) Else If arr[l..mid] is sorted
        a) If key to be searched lies in range from arr[l]
           to arr[mid], recur for arr[l..mid].
        b) Else recur for arr[mid+1..r]
    4) Else (arr[mid+1..r] must be sorted)
        a) If key to be searched lies in range from arr[mid+1]
           to arr[r], recur for arr[mid+1..r].
        b) Else recur for arr[l..mid] 
        
Reference see from [Search an element in a sorted and rotated array](http://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-pivoted-array/), this idea is the same from the solution in the book. (See P399)

 
     class Solution(object):
        def search(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: int
            """
            return self.bsearch(nums, target, 0, len(nums)-1)

        def bsearch(self, nums, x, l, h):
            if l > h:
                return -1
            mid = (l + h) / 2
            if nums[mid] == x:
                return mid
            if nums[l] <= nums[mid]:
                #nums[l..mid] is sorted
                if x >= nums[l] and x < nums[mid]:
                    return self.bsearch(nums, x, l, mid-1)
                return self.bsearch(nums, x, mid+1, h)
            # if nums[l..mid] is not sorted, then arr[mid..h] must be sorted
            if x > nums[mid] and x <= nums[h]:
                return self.bsearch(nums, x, mid+1, h)
            return self.bsearch(nums, x, l, mid-1)
                    
            