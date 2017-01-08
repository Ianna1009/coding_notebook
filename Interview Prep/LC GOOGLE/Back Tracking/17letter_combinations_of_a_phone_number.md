## 17. Letter Combinations of a Phone Number


Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

![](200px-Telephone-keypad2.svg.png)

    Input:Digit string "23"
    Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

**Note:**

Although the above answer is in lexicographical order, your answer could be in any order you want.

**Ideas:**

1. According to basic back tracking idea, we need to find valid condition space to search: here once we make sure of the first letter we should use, choices we have for the next letter is made. Then those choices should be our valid conditions.
2. Since for each key on the phone, we need to be clear the choices we have for a key. Therefore we need a "look-up table" (implemented with a dictionary here) to easily get those valid choices.

**Solution:**

    TC: O(2^n) SC: O(n)
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        res = []
        if len(digits) == 0:
            return res
        teleDict = {'1': '*', '2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl', '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz', '0': ' '}
        self.getCombinations(digits, res, teleDict, "")
        return res
    
    def getCombinations(self, d, res, t, tmp):
        if len(d) == 0:
            res.append(tmp)
            return
        for i in t[d[0]]:
            self.getCombinations(d[1:], res, t, tmp+i)
        
            
            
            
            
            
