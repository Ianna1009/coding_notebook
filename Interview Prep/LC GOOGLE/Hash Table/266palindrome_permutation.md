## 266.Palindrome Permutation

Given a string, determine if a permutation of the string could form a palindrome.

**For example,**

    "code" -> False, "aab" -> True, "carerac" -> True.
    
**Solution #1:**

    def canPermutePalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        n = len(s)
        count = 0
        h = collections.defaultdict(int)
        for i in xrange(n):
            h[s[i]] += 1
            if h[s[i]] % 2:
                count += 1
            else:
                count -= 1
        if n % 2 and count > 1 or n % 2 == 0 and count != 0:
            return False
        return True
        
**Solution #2:**

    class Solution(object):
        def canPermutePalindrome(self, s):
            """
            :type s: str
            :rtype: bool
            """
            cont = collections.Counter(s)
            odd = 0
            for ch in cont:
                if cont[ch] % 2:
                    if odd == 0:
                        odd += 1
                    else:
                        return False
            return True
        

            
