## 10.1 Sorted Merge

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

**Note:**

You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

**Idea:**

Since we know that A has enough buffer at the end, we won't need to allocate additional space. Our logic should involve simply comparing elements of A and B and inserting them in order, until we've exhausted all elements in A and in B.

The only issue with this is that if we insert an element into the front of A, then we'll have to shift the existing elements backwards to make room for it. It's better to insert elements into the back of the array, where there's empty space.

The code below does just that. It workd from the back of A and B, moving the largest elements to the back of A.

---
**Solution: Two Pointers**

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
                elif j >= 0:
                    nums1[k] = nums2[j]
                    j -= 1
                k -= 1

Note that you don't need to copy the contents A after running out of elements in B. They are already in place.
But you **must** copy content B after running out of A. Otherwise the following case won't work:

    A = [1], m = 0
    B = [2], n = 1


            

