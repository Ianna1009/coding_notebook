## 370. Range Addition

Assume you have an array of length n initialized with all 0's and are given k update operations.

Each operation is represented as a triplet: [startIndex, endIndex, inc] which increments each element of subarray A[startIndex ... endIndex] (startIndex and endIndex inclusive) with inc.

Return the modified array after all k operations were executed.

**Example:**

    Given:
    
        length = 5,
        updates = [
            [1,  3,  2],
            [2,  4,  3],
            [0,  2, -2]
        ]
    
    Output:
    
        [-2, 0, 3, 5, 3]
**Explanation:**

    Initial state:
    [ 0, 0, 0, 0, 0 ]
    
    After applying operation [1, 3, 2]:
    [ 0, 2, 2, 2, 0 ]
    
    After applying operation [2, 4, 3]:
    [ 0, 2, 5, 5, 3 ]
    
    After applying operation [0, 2, -2]:
    [-2, 0, 3, 5, 3 ]
    
**Naive Solution(TLE):**

    class Solution(object):
        def getModifiedArray(self, length, updates):
            """
            :type length: int
            :type updates: List[List[int]]
            :rtype: List[int]
            """
            init_array = [0 for _ in xrange(length)]
            for startInd, endInd, num in updates:
                for i in xrange(startInd, endInd+1):
                    init_array[i] += num
            return init_array
            
**Notes:**

1. When updating frequently at a very large length of array, the result gets TLE since it took O(n^2) time worst case.
2. According to the hint, we can implement it within O(n+k) time, where n is the length of array and k is the number of updates.

    **Hint:**

    Thinking of using advanced data structures? You are thinking it too complicated.
    For each update operation, do you really need to update all elements between i and j?
    Update only the first and end element is sufficient.
    The optimal time complexity is O(k + n) and uses O(1) extra space. 
    
**Solution #2:**

    class Solution(object):
        def getModifiedArray(self, length, updates):
            """
            :type length: int
            :type updates: List[List[int]]
            :rtype: List[int]
            """
            array = [0 for _ in xrange(length)]
            for start, end, num in updates:
                array[start] += num
                if end < length - 1:
                    array[end+1] -= num
                    
            value = 0
            for i in xrange(length):
                value += array[i]
                array[i] = value
            return array
            
**Notes:**

1. The reason we update value(`+inc`) at the start index is that we need to update every item since this index.
2. The reason we update value(`-inc`) at the end+1 index is that we previously has added `inc` already which is unnecessary, thus we need to subtract `inc` such that from this index on, we no longer need to add `inc` on following items in the array.
3. After all, every time we update, we should update `array[start]` by adding `inc` and update `array[end]` by subtracting `inc`. Once we kept track of every update, we should iterate the whole array by summing up all previous items at index `i` then set up `array[i]` with this sum.


        