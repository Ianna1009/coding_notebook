## LC316.Remove Duplicate Letters

Given a string which contains only lowercase letters, remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in **lexicographical order** among all possible results.

**Example:**

    Given "bcabc"
    Return "abc"

    Given "cbacdcbc"
    Return "acdb"

---

** Note: **

不能改变原字符串的顺序，只是去重。

** Solution (Recursive): **

    class Solution(object):
        def removeDuplicateLetters(self, s):
            """
            :type s: str
            :rtype: str
            """
            for ch in sorted(set(s)):
                suffix = s[s.index(ch):]
                if set(suffix) == set(s):
                    return ch + self.removeDuplicateLetters(suffix.replace(ch, ""))
            return ""


** Solution (Stack):**

    from collections import Counter

    class Solution(object):
        def removeDuplicateLetters(self, s):
            """
            :type s: str
            :rtype: str
            """
            counter = collections.Counter(s)
            res = set()
            stack = []
            for ch in s:
                counter[ch] -= 1
                if ch in res:
                    continue
                while stack and stack[-1] > ch and counter[stack[-1]]:
                    res.remove(stack.pop())
                res.add(ch)
                stack.append(ch)
            return ''.join(stack)
