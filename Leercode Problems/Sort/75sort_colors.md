## 75. Sort Colors

Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note:
You are not suppose to use the library's sort function for this problem.

**Ideas:**
1. One pass will be using a simply two-pointers strategy. 
2. Start pointer points at end of red objects, end pointer points at the beginning of the blue objects.
3. Each time meets with a blue object, swap(end, i), then end pointer -= 1
4. Each time meets with a red object, swap(start, i), then start pointer += 1

---
**Solution:**

    class Solution(object):
        def sortColors(self, nums):
            """
            :type nums: List[int]
            :rtype: void Do not return anything, modify nums in-place instead.
            """
            n = len(nums)
            # end pointer always point to the start of blue objects, and start to the red ones.
            start, end = 0, n-1
            i = 0
            while i < end+1:
                if nums[i]  == 2:
                    nums[i], nums[end] = nums[end], nums[i]
                    end -= 1
                    continue
                elif nums[i] == 0:
                    nums[start], nums[i] = nums[i], nums[start]
                    start += 1
                    i += 1
                    continue
                i += 1
                
**Explanation:**   
Initial Array:

| *1* | 2 | 0 | 1 | *0* |
| -- | -- | -- | -- | -- |
| start |  |  |  | end |
| i = 0  |

`nums[i]` is white, i += 1, continue

| 1 | *2* | 0 | 1 | *0* |    
| -- | -- | -- | -- | -- |       
| start |  |  |  | end |       
|  | i = 1|           

`nums[i]` is a blue one, {swap(nums[i], nums[end]), end -= 1}, i += 1

| *1* | 0 | *0* | 1 | 2 |
| -- | -- | -- | -- | -- |
| start |  |  | end |  | 
|  | | i = 2|
      
`nums[i]` is a red one, {swap(nums[i], nums[start]), start += 1, ***i += 1***}, i += 1

| 0 | 0 | 1 | 1 | *2* |
| -- | -- | -- | -- | -- |
|  | start |  | end |  | 
|  | | | | i = 4| 

`nums[i]` is a red one, swap(nums[i], nums[start]), start += 1, **i += 1**
