##373. Find K Pairs with Smallest Sums 

You are given two integer arrays nums1 and nums2 sorted in ascending order and an integer k.

Define a pair (u,v) which consists of one element from the first array and one element from the second array.

Find the k pairs (u1,v1),(u2,v2) ...(uk,vk) with the smallest sums.

**Example 1:**

    Given nums1 = [1,7,11], nums2 = [2,4,6],  k = 3
    
    Return: [1,2],[1,4],[1,6]
    
    The first 3 pairs are returned from the sequence:
    [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
**Example 2:**

    Given nums1 = [1,1,2], nums2 = [1,2,3],  k = 2
    
    Return: [1,1],[1,1]
    
    The first 2 pairs are returned from the sequence:
    [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
**Example 3:**
   
    Given nums1 = [1,2], nums2 = [3],  k = 3 
    
    Return: [1,3],[2,3]
    
    All possible pairs are returned from the sequence:
    [1,3],[2,3]
    
**Ideas:**

1. One way to get k smallest sums is to use heap.
2. Since we need to use max-heap, we will import `heapq`(min-heap) and -sum as our key value.

**Solution(Heap):**

    import heapq
    
    class Solution(object):
        def kSmallestPairs(self, nums1, nums2, k):
            """
            :type nums1: List[int]
            :type nums2: List[int]
            :type k: int
            :rtype: List[List[int]]
            """
            # store result in a max heap with size k
            heap = []
            for i in xrange(len(nums1)):
                for j in xrange(len(nums2)):
                    x, y = nums1[i], nums2[j]
                    if len(heap) < k:
                        heapq.heappush(heap, (-(x+y), [x, y]))
                    elif -(x+y) > heap[0][0]:
                        heapq.heappushpop(heap, (-(x+y), [x,y]))
            return [pair for neg_sum, pair in heap]
            
**Notes:**

Just be careful of using `heappushpop`, whenever `sum < heap[0]`, we push in `sum`. Therefore, `when -sum > heap[0]: heapq.heappushpop(heap, (-sum, [x, y])`.

**Modified Solution:**

    class Solution(object):
        def kSmallestPairs(self, nums1, nums2, k):
            """
            :type nums1: List[int]
            :type nums2: List[int]
            :type k: int
            :rtype: List[List[int]]
            """
            ans = []
            heap = [(0x7FFFFFFF, None, None)]
            size1, size2 = len(nums1), len(nums2)
            idx2 = 0
            while len(ans) < min(k, size1 * size2):
                if idx2 < size2:
                    sum, i, j = heap[0]
                    if nums2[idx2] + nums1[0] < sum:
                        for idx1 in range(size1):
                            heapq.heappush(heap, (nums1[idx1] + nums2[idx2], idx1, idx2))
                        idx2 += 1
                sum, i, j = heapq.heappop(heap)
                ans.append((nums1[i], nums2[j]))
            return ans

**Still updating** This second solution referred to ["书影博客"](http://bookshadow.com/weblog/2016/07/07/leetcode-find-k-pairs-with-smallest-sums/)    

    



















