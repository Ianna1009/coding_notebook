## LC56.Merge Intervals

Given a collection of intervals, merge all overlapping intervals.

**For example**,

    Given [1,3],[2,6],[8,10],[15,18],
    return [1,6],[8,10],[15,18].

---
** Solution:**

    # Definition for an interval.
    # class Interval(object):
    #     def __init__(self, s=0, e=0):
    #         self.start = s
    #         self.end = e

    class Solution(object):
        def merge(self, intervals):
            """
            :type intervals: List[Interval]
            :rtype: List[Interval]
            """
            res = []
            if len(intervals) == 0:
                return res
            intervals = sorted(intervals, key = lambda x: x.start)
            res.append(intervals[0])
            for item in intervals:
                prev = res[-1]
                # 第一种情况：两个interval不相交：
                if prev.end < item.start:
                    res.append(item)
                # 第二种情况： 两个interval相交，取第一个的start和第二个的end为端点
                elif prev.end < item.end:
                    prev.end = item.end
                    res.pop()
                    res.append(prev)
            return res