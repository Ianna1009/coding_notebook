## 338.Counting Bits

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

**Example:**
    
    For num = 5 you should return [0,1,1,2,1,2].

**Follow up:**

* It is very easy to come up with a solution with run time `O(n*sizeof(integer))`. But can you do it in linear time O(n) /possibly in a single pass?
* Space complexity should be O(n).
* Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.


**Solution: (Naive DP)**

    def countBits(self, num):
        """
        :type num: int
        :rtype: List[int]
        """
        if num < 2:
            return [0, 1] if num == 1 else [0]
        total = [0, 1]
        for i in xrange(2, num+1):
            if i % 2 == 0:
                total.append(total[i/2])
            else:
                total.append(total[i/2] + 1)
        return total