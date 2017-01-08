# LC356.Line Reflection


Given n points on a 2D plane, find if there is such a line parallel to y-axis that reflect the given points.

    Example 1:
    Given points = [[1,1],[-1,1]], return true.

    Example 2:
    Given points = [[1,1],[-1,-1]], return false.
___
**Solution:**

    class Solution(object):
        def isReflected(self, points):
            """
            :type points: List[List[int]]
            :rtype: bool
            """
            h = set([(x[0], x[1]) for x in points]) ## Remove Duplicates
            l = sorted([x for x in h])
            return l == sorted((l[0][0] + l[-1][0] - x, y) for x,y in l)
            
---
** Solution_2:(w/o sort, just using hashtable)**

    from sets import Set
    class Solution(object):
        def isReflected(self, points):
            """
            :type points: List[List[int]]
            :rtype: bool
            """
            MAX, MIN = -float('inf'), float('inf')
            hashMap = {}
            for i in xrange(len(points)):
                MAX = max(points[i][0], MAX)
                MIN = min(points[i][0], MIN)
                if points[i][1] not in hashMap:
                    hashMap[points[i][1]] = Set([points[i][0]])
                else:
                    hashMap[points[i][1]].add(points[i][0])
            for i in xrange(len(points)):
                if (points[i][1] not in hashMap) or ((MAX + MIN - points[i][0]) not in hashMap[points[i][1]]):
                    return False
            return True