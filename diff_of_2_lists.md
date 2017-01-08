## Diff of 2 Lists

Given two lists A and B, return A - B and B - A correspondingly.

For example:

    A = [1, 3, 4, 1, 6, 3]
    B = [2, 3, 1]
should return:

    A - B =  [1, 3, 4, 6]
    B - A =  [2] 
    
---

** Solution: **

    from collections import Counter
    
    class Solution(object):
    
        def diff(self, l1, l2):
            res = []
            c1 = Counter(l1)
            c2 = Counter(l2)
            for item in c2:
                if item not in c1:
                    continue
                else:
                    c1[item] -= 1
            for x in c1:
                res += [x for _ in xrange(c1[x])]
            return res
                