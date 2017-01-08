## 8.3 Magic Index

A magic index in an array `A[1, ..., n-1]` is defined to be an index such that A[i] = i. Given a sorted array of distinct integers, write a method to find a magic index, if one exists, in array A.

**Follow up:**

What if the values are not distinct?

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| -2 | -1 | 0 | 2 | 2 | 3 | 5 | 7 | 9 | 12 |


**Solution #1: **

Given that the array is sorted, we may use binary search. 
1. If A[mid] < mid: recursion on the right (mid+1, end)
2. Elif A[mid] > mid: recursion on the left (start, mid-1)
3. Else: A[mid] == mid: return mid.


    def magicBS(self, arr):
        if len(arr) == 0:
            return None
        start, end = 0, len(arr) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if arr[mid] < mid:
                start = mid + 1
            elif arr[mid] > mid:
                end = mid - 1
            else:
                return mid
        if arr[start] == start:
            return start
        if arr[end] == end:
            return end
        return None
---
(Solution using dfs):
    
    def magicBS(self, arr):
        return self.searcher(arr, 0, len(arr)-1)
        
    def searcher(Self, arr, start, end):
        if end < start:
            return -1
        mid = (start + end) / 2
        if arr[mid] == mid:
            return mid
        elif arr[mid] > mid:
            return self.searcher(arr, 0, mid-1)
        else:
            return self.searcher(arr, mid+1, end)
   
   
  **Follow-Up: What if the elements are not distinct?**
  
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| -1 | -1 | **2** | **2** | **2** | 4 | 5 | 7 | 9 | 12 |

When we see that A[mid] < mid, we can't conclude which side the magic index in on. It could be on the right side, as before. Or it could be on the left side (as it, in fact, is).

Could it be anywhere on the left side? Not exactly, since A[4] = 2, we know that A[3] couldn't be on the magic index. A[3] would need to be 3 to be the magic index, but A[3] must be less than or equal to A[4].

In fact, when we see that A[4] = 2, we'll need to recursively search the right side as before. But, to search the left side, we can skip a bunch of elements and only recursively search elements A[0] through A[2]. A[2] could be the first element that could be a magic index.

The general pattern is that we compare `midIndex` and `midValue` for equality first. Then, if they are not equal, we recursively search the left and right sides as follows:

  * Left side: search indices start through Math.min(midIndex-1, midValue).
  * Right side: search indices Math.max(midIndex + 1, midValue) through end.

The code below implements this algorithm:

    def magicFast(self, arr):
        return self.searcher(arr, 0, len(arr)-1)
        
    def searcher(self, arr, start, end):
        if end < start:
            return -1
        midIndex = (start + end) / 2
        midValue = arr[midIndex]
        if midValue == miIndex:
            return midIndex
        # Search left:
        leftIndex = min(midIndex - 1, midValue)
        left = self.searcher(array, start, ledtIndex)
        if left >= 0:
            return left
            
        # Search right:
        rightIndex = max(midIndex + 1, midValue)
        right = self.searcher(arr, rightIndex, end)
        return right
        
**Note that on the above solution, if the elements are all distinct, the method operated almost identically to the first solution.**
            


        
   