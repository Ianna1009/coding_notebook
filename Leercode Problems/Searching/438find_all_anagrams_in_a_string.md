## 438.Find All Anagrams in a String

Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

Example 1:

    Input:
    s: "cbaebabacd" p: "abc"

    Output:
    [0, 6]

    Explanation:
    The substring with start index = 0 is "cba", which is an anagram of "abc".
    The substring with start index = 6 is "bac", which is an anagram of "abc".
Example 2:

    Input:
    s: "abab" p: "ab"

    Output:
    [0, 1, 2]

    Explanation:
    The substring with start index = 0 is "ab", which is an anagram of "ab".
    The substring with start index = 1 is "ba", which is an anagram of "ab".
    The substring with start index = 2 is "ab", which is an anagram of "ab".
    
**Attemp #1: (TLE)**

    class Solution(object):
    
        def findAnagrams(self, s, p):
            n = len(p)
            i, j = 0, n
            h = "".join(sorted(p))
            res = []
            while j <= len(s):
                sub = s[i:j]
                sub_sorted = "".join(sorted(sub))
                if sub == p or sub_sorted == h:
                    res.append(i)
                i += 1
                j += 1
            return res
This brute force algorithm will cost O(n*mlgm) time, where m is the length of string `p` and n is the length of string `s`.
 
Reference to the [method](http://www.geeksforgeeks.org/anagram-substring-search-search-permutations/) using Rabin Karp Algorithm. 

**Attempt #2: **