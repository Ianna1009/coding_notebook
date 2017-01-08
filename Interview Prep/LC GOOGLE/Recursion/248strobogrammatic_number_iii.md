## 248.Strobogrammatic Number III

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Write a function to count the total strobogrammatic numbers that exist in the range of low <= num <= high.

**For example,**

      Given low = "50", high = "100", return 3. Because 69, 88, and 96 are three strobogrammatic numbers.

**Note:**
Because the range might be a large number, the low and high numbers are represented as string.

**Solution:**

    def strobogrammaticInRange(self, low, high):
        """
        :type low: str
        :type high: str
        :rtype: int
        """
        h = {'0': '0', '1': '1', '6': '9', '8': '8', '9': '6'}
        res = []
        if n % 2 == 0:
            self.finder(n, h, res, "")
        else:
            h2 = ['0', '1', '8']
            for j in h2:
                self.finder(n-1, h, res, j)
        return res
    
    def finder(self, n, h, res, num):
        if n == 0:
            if num[0] == '0' and len(num) > 1:
                return
            res.append(num)
            return
        for i in h:
            new = i + num + h[i]
            self.finder(n-2, h, res, new)        