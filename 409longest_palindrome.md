## 409.Longest Palindrome

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

**Note:**
Assume the length of given string will not exceed 1,010.

**Example:**

      Input:
      "abccccdd"

      Output:
      7

    Explanation:
    One longest palindrome that can be built is "dccaccd", whose length is 7.
    
**Solution: **

    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: int
        """
        cont = collections.Counter(s)
        res = 0
        odd = 0
        for char in cont:
            if cont[char] % 2 == 0:
                res += cont[char]
            else:
                if odd == 0:
                    res += 1
                    odd += 1
        return res

First Round -- Wrong Answer: "ccc"

    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: int
        """
        cont = collections.Counter(s)
        res = 0
        odd = 0
        for char in cont:
            c = cont[char]
            if c % 2 == 1 and odd == 0:
                odd += 1
                res += 1
            while c > 1:
                c -= 2
                res += 2
        return res
        
Second Round: Accepted

Some other solution from: http://bookshadow.com/weblog/2016/10/02/leetcode-longest-palindrome/

    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: int
        """
        cont = collections.Counter(s)
        res = 0
        odd = 0
        for c in cont:
            res += cont[c]
            if cont[c] % 2 == 1:
                odd += 1
                res -= 1
        return res + (odd > 0)
                
                
                