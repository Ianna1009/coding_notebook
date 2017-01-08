## 1.2 Check Permutation

Given two strings, write a method to decide if one is permutation of the other.

**Note:**

Make sure with the interviewee:
1. **Case sensitive** or not.
    For example, is 'God' a permutation of 'dog'?
2. Is **whiteSpace** significant?
    For example: is 'go    d' a permutation of 'dog'?
    
Assume case sensitive and white-space is significant. 
    
**Solution #1 (Sort the strings if you can make changes on strings): **

    def checkPerms(self, s1, s2):
        # Check lengths:
        if len(s1) != len(s2):
            return False
        s1.sort()
        s2.sort()
        return s1 == s2
        
**Solution #2: (Using counter if you can use additional space)**

    def checkPerms(self, s1, s2)
        # Check lengths:
        if len(s1) != len(s2):
            return False
        d1 = collections.Counter(s1)
        for c in s2:
            if c not in d1 or d1[c] == 0:
                return False
            di[c] -= 1
        return True
        

