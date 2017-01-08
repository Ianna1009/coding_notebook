## 10.3/LC81. Search in Rotated Array with duplicates

Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

As in the example array `{2, 2, 2, 3, 4, 2}`. 

In this case, we can check if the **rightmost element** is different. If it is, we can search just the right side. Otherwise we have no choice but to search both halves.



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
                return False
            mid = (l + h) / 2
            if nums[mid] == x:
                return True
            if nums[l] < nums[mid]:
                #nums[l..mid] is sorted
                if x >= nums[l] and x < nums[mid]:
                    return self.bsearch(nums, x, l, mid-1)
                return self.bsearch(nums, x, mid+1, h)
            # if nums[l..mid] is not sorted, then arr[mid..h] must be sorted
            elif nums[mid] < nums[l]:
                if x > nums[mid] and x <= nums[h]:
                    return self.bsearch(nums, x, mid+1, h)
                return self.bsearch(nums, x, l, mid-1)
            
            
            # left or right half is all repeats
            elif nums[l] == nums[mid]:
                # if right is different, search it
                if nums[mid] != nums[h]:
                    return self.bsearch(nums, x, mid+1, h)
                # else, we'll have to search both halves
                else:
                    res = self.bsearch(nums, x, l, mid-1)
                    if not res:
                        return self.bsearch(nums, x, mid+1, h)
                    else:
                        return res
                        
**Answer to Follow-ups:**

This code will run O(lgn) if all elements are unique. However, with many duplicates, the algorithm is actually **O(n)**. This is because with many duplicates, we will often have to search both the left and right sides of the array(or sub-arrays).

Note that while this problem is not conceptually very complex, it is actually very difficult to implement flawlessly. Don't feel bad if you had trouble implementing it without a few bugs. Because of the case of making off-by-one and other minor errors, you should make sure to test your code very thoroughly. 
                
                    
                
        
