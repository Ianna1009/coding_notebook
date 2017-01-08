## 247.Strobogrammatic Number II

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Find all strobogrammatic numbers that are of length = n.

For example,
Given n = 2, return ["11","69","88","96"].

**Solution: **

    def findStrobogrammatic(self, n):
        """
        :type n: int
        :rtype: List[str]
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
            
        