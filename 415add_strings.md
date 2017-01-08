## 415.Add Strings

Given two non-negative numbers num1 and num2 represented as string, return the sum of num1 and num2.

**Note:**

1. The length of both num1 and num2 is < 5100.
2. Both num1 and num2 contains only digits 0-9.
3. Both num1 and num2 does not contain any leading zero.
4. You must not use any built-in BigInteger library or convert the inputs to integer directly.

**Solution: **

    def addStrings(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        """
        int1, int2 = self.strToInt(num1), self.strToInt(num2)
        return str(int1 + int2)
        
        
    def strToInt(self, s):
        h = {'1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9, '0': 0}
        res = 0
        for c in s:
            res *= 10
            res += h[c]
        return res
        
**Solution (correct):**

    def addStrings(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        """
        res = []
        carry = 0
        m, n = len(num1), len(num2)
        while m or n or carry:
            s = carry
            if m:
                m -= 1
                s += int(num1[m])
            if n:
                n -= 1
                s += int(num2[n])
            carry = 1 if s > 9 else 0
            res.append(str(s%10))
        return "".join(res[::-1])
