## 451. Sort Characters By Frequency

Given a string, sort it in decreasing order based on the frequency of characters.

**Example 1:**

    Input:
    "tree"
    
    Output:
    "eert"
    
    Explanation:
    'e' appears twice while 'r' and 't' both appear once.
    So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
**Example 2:**

    Input:
    "cccaaa"
    
    Output:
    "cccaaa"
    
    Explanation:
    Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
    Note that "cacaca" is incorrect, as the same characters must be together.
**Example 3:**

    Input:
    "Aabb"
    
    Output:
    "bbAa"
    
    Explanation:
    "bbaA" is also a valid answer, but "Aabb" is incorrect.
    Note that 'A' and 'a' are treated as two different characters.
    
**Ideas:**

1. counter must be used.
2. This is similar to the problem of getting the most frequency number in of sequence. Thanks to "[书影博客](http://bookshadow.com/weblog/2016/11/02/leetcode-sort-characters-by-frequency/)": I've learnt a new method to combine getting mode and pop together: counter.most_common()

**Solution #1:**

    class Solution(object):
        def frequencySort(self, s):
            """
            :type s: str
            :rtype: str
            """
            char_count = collections.Counter(s)
            return "".join(ch * cont for ch, cont in char_count.most_common())
            
**Solution #2:**


