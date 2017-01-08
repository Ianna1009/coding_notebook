## 164. Maximum Gap

Given an unsorted array, find the maximum difference between the successive elements in its sorted form.

Try to solve it in **linear time/space**.

Return 0 if the array contains less than 2 elements.

You may assume all elements in the array are non-negative integers and fit in the 32-bit signed integer range.


**Ideas: **

Linear Time would make us think of bucket sort. It's also easier to think about using ceiling[(MAX - MIN)/(len(nums)-1)] as the number of one bucket, at most there will be (MAX - MIN)/len(nums) + 1 buckets.

In each bucket, the range will be (MAX - MIN) / len(nums), int((MAX - MIN - 1) / (len(nums) - 1)) + 1 ensures the widest range.


---
Solution:

    class Solution(object):
        def maximumGap(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            if len(nums) < 2:
                return 0
            MIN, MAX = nums[0], nums[0]
            for i in nums:
                MIN = min(i, MIN)
                MAX = max(i, MAX)
            bucketRange = max(1, int((MAX - MIN - 1) / (len(nums) - 1)) + 1)
            bucketLen = (MAX - MIN) / bucketRange + 1
            b = [None for _ in xrange(bucketLen)]
            for i in nums:
                loc = (i - MIN) / bucketRange
                if b[loc] is None:
                    b[loc] = {'MIN': i, 'MAX': i}
                else:
                    b[loc]['MIN'] = min(i, b[loc]['MIN'])
                    b[loc]['MAX'] = max(i, b[loc]['MAX'])

            maxGap = 0
            for i in xrange(bucketLen):
                if b[i] is None:
                    continue
                j = i + 1
                while j < bucketLen and b[j] is None:
                    j += 1
                if j < bucketLen:
                    maxGap = max(maxGap, b[j]['MIN'] - b[i]['MAX'])
                i = j
            return maxGap
            

