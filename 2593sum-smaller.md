## 259. 3Sum Smaller

Given an array of n integers nums and a target, find the number of index triplets i, j, k with `0 <= i < j < k < n` that satisfy the condition `nums[i] + nums[j] + nums[k] < target`.

**For example,** 

    given `nums = [-2, 0, 1, 3]`, and `target = 2`.

    Return 2. Because there are two triplets which sums are less than 2:

    [-2, 0, 1]
    [-2, 0, 3]
**Follow up:**

Could you solve it in O(n2) runtime?

**Ideas:**

3Sum problems are all similar, we can use two pointers once we fix one out of three numbers in the valid triplets. This will take O(n^2) time

1. Outer loop is getting the first valid number, thus in range 0..n-2
2. Once first number fixed, `low` and `high` are pointing at the beginning and ending of the rest array.
    * If `nums[low] + nums[high] < target - first`: 
        * all pairs [low, i] (i <= high) are valid, thus this many valid solution -- high-low -- will be added to result.
        * low += 1
    * Else:
        * high -= 1
         
**Solution:**

    class Solution(object):
        def threeSumSmaller(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: int
            """
            res = 0
            nums.sort()
            for i in xrange(len(nums)-2):
                # Fix one number
                first = nums[i]
                val = target - first
                # Use two pointers on the rest array to find valid answers
                low, high = i+1, len(nums)-1
                while low < high:
                    x, y = nums[low], nums[high]
                    if x+y < val:
                        res += (high-low)
                        low += 1
                    else:
                        high -= 1
            return res

After cleaning it up, solution gets more clear:

**Solution (clean):**

    class Solution(object):
        def threeSumSmaller(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: int
            """
            cont, n = 0, len(nums)
            nums.sort()
            for i in xrange(n-2):
                j, k = i+1, n-1
                while j < k:
                    if nums[j] + nums[k] + nums[i] < target:
                        # Note that k-j possible solutions
                        cont += k-j
                        j += 1
                    else:
                        k -= 1
            return cont
                        
            
        