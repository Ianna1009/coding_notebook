## 66.Plus One

Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.

**Solution #1 (Recursion)**

    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        n = len(digits)
        if n == 0:
            return 1
        res = []
        self.helper(digits, res, [])
        return res[0]
        
    def helper(self, digits, res, tmp):
        if len(digits) == 0:
            tmp.append(1)
            res.append([]+tmp[::-1])
            return
        last = digits[-1]
        if last < 9:
            tmp.append(last+1)
            res.append(digits[:-1]+tmp[::-1])
            return
        self.helper(digits[:-1], res, tmp + [0])
        
**Solution #2 (Naive)**
        
        
        