## Merge K Sorted Arrays

第二题: 已知k个sorted array of int, return 一个 sorted array. 其中每个array的average size是N. 用Heap(priority queue)做，O(Nklogk)时间O(Nk)空间。

First, let's take a look at [LC88. Merge Two Sorted Arrays.](https://leetcode.com/problems/merge-sorted-array/)

Two pointers, both starting from the** ends **of two arrays. 
** Assumption: List 1 is large enough. **

    class Solution(object):
        def merge(self, nums1, m, nums2, n):
            """
            :type nums1: List[int]
            :type m: int
            :type nums2: List[int]
            :type n: int
            :rtype: void Do not return anything, modify nums1 in-place instead.
            """
            i, j = m-1, n-1
            k = m + n - 1
            while k >= 0:
                if i >= 0 and j >= 0:
                    if nums1[i] > nums2[j]:
                        nums1[k] = nums1[i]
                        i -= 1
                    else:
                        nums1[k] = nums2[j]
                        j -= 1
                elif i >= 0:
                    nums1[k] = nums1[i]
                    i -= 1
                elif j >= 0:
                    nums1[k] = nums2[j]
                    j -= 1
                k -= 1

---
Then for this merging with K lists:

Problem Link: [Merge k sorted arrays | Set 1](http://www.geeksforgeeks.org/merge-k-sorted-arrays/)

Given k sorted arrays of size n each, merge them and print the sorted output.

**Example:**

    Input:
    k = 3, n =  4
    arr[][] = { {1, 3, 5, 7},
                {2, 4, 6, 8},
                {0, 9, 10, 11}} ;

    Output: 0 1 2 3 4 5 6 7 8 9 10 11 

A simple solution is to create an output array of size n*k and one by one copy all arrays to it. Finally, sort the output array using any O(nLogn) sorting algorithm. This approach takes O(nkLognk) time.

**We can merge arrays in O(nk*Logk) time using Min Heap. Following is detailed algorithm.**
1. Create an output array of size n*k.
2. Create a min heap of size k and insert 1st element in all the arrays into a the heap
3. Repeat following steps n*k times.
     a) Get minimum element from heap (minimum is always at root) and store it in output array.
     b) Replace heap root with next element from the array from which the element is extracted. If the array doesn’t have any more elements, then replace root with infinite. After replacing the root, heapify the tree.
     
** Solution: **


    import heapq
    class Solution():

        def MergeKArrays(self, arrs):
            # arrsType: list(lists)
            # k: the number of lists
            # n: the length of list in arrs
            res = []
            h = []
            k = len(arrs)
            """
            res for results
            h is a heap list with length k
            """
            for j in xrange(k):
                heapq.heappush(h, (arrs[j][0], j, 0))
            # Push the first number into Minheap
            while h[0][0] != float('inf'):
                num, arr_index, num_index = heapq.heappop(h)
                res.append(num)
                num_index += 1
                if num_index < len(arrs[arr_index]):
                    heapq.heappush(h, (arrs[arr_index][num_index], arr_index, num_index))
                else:
                    heapq.heappush(h, (float('inf'), arr_index, num_index))
            return res

