## 8.9 Parens

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, 

    given n = 3, a solution set is:
    
    [
      "((()))",
      "(()())",
      "(())()",
      "()(())",
      "()()()"
    ]
    
**Solution of mine:**
    
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        res = []
        self.generater(res, 2*n, "", n, n)
        return res
        
    def generater(self, res, n, tmp, left, right):
        if n == 0:
            res.append(tmp)
            return
        if left > 0:
            self.generater(res, n-1, tmp+"(", left-1, right)
        if left < right:
            self.generater(res, n-1, tmp+")", left, right-1)
            
            
**Solution from the book: **

    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        res = []
        self.generater(res, 2*n, "", n, n)
        return res
        
    def generater(self, res, n, tmp, leftRem, rightRem):
        if leftRem < 0 or leftRem > rightRem:
            return
        if leftRem == 0 and rightRem == 0:
            res.append(tmp)
            return
        self.generater(res, n-1, tmp+"(", leftRem-1, rightRem)
        self.generater(res, n-1, tmp+")", leftRem, rightRem-1)