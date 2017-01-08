## 459.Repeated Sub-string Pattern

Given a non-empty string check if it can be constructed by taking a sub-string of it and appending multiple copies of the sub-string together.

You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

**Example 1:**

    Input: "abab"

    Output: True

    Explanation: It's the substring "ab" twice.
**Example 2:**

    Input: "aba"

    Output: False
**Example 3:**

    Input: "abcabcabcabc"

    Output: True

    Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)
    
**Ideas:**

1. In 'abcabc' each character appears even number of times. And for the same character, the difference between it's indeices should correspond to the following character. For example: {'a': [0, 3], 'b': [1, 4], 'c': [2, 5]}.
2. In 'aba', 'b' appears only once, which means the length of its indices list differs from 'a''s.
3. In 'abba', although the length of each character indices list is the same, but they are not from the same sequence. ([0, 3] and [1, 2])
4. In 'aabaab', indices lists will be like: {'a': [0,1,3,4], 'b': [2,5]}. How should we check this case?

**Solution: (Refer to http://bookshadow.com/weblog/2016/11/13/leetcode-repeated-substring-pattern/)**

    def repeatedSubstringPattern(self, str):
        """
        :type str: str
        :rtype: bool
        """
        n = len(str)
        for i in xrange(1, n/2+1):
            if n % i:
                continue
            else:
                if str[:i] * (n/i) == str:
                    return True
        return False