## 242. Valid Anagram

Given two strings s and t, write a function to determine if t is an anagram of s.

    For example,
    s = "anagram", t = "nagaram", return true.
    s = "rat", t = "car", return false.

**Note:**
You may assume the string contains only lowercase alphabets.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?

---
Approach #1 (Sort and Compare):

    class Solution(object):
        def isAnagram(self, s, t):
            """
            :type s: str
            :type t: str
            :rtype: bool
            """
            return sorted([x for x in s]) == sorted([y for y in t])

Approach #2 (HashTable)

    class Solution(object):
        def isAnagram(self, s, t):
            """
            :type s: str
            :type t: str
            :rtype: bool
            """
            h = {}
            if len(s) != len(t):
                return False
            for i in xrange(len(s)):
                h[s[i]] = h.get(s[i], 0) + 1
                h[t[i]] = h.get(t[i], 0) - 1

            for i in h:
                if h[i] != 0:
                    return False
            return True


            
            
            