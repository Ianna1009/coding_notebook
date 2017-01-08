## 252. Meeting Rooms

Given an array of meeting time intervals consisting of start and end times `[[s1,e1],[s2,e2],...] (si < ei)`, determine if a person could attend all meetings.

For example,
    
    Given [[0, 30],[5, 10],[15, 20]],
    return false.
    
    
**Ideas:**

It's the simpler version of **Merge Interval**, the easiest way to think of it is to sort intervals by their starts.

---
**Solution #1: sort method in O(n lg n)**

    # Definition for an interval.
    # class Interval(object):
    #     def __init__(self, s=0, e=0):
    #         self.start = s
    #         self.end = e

    class Solution(object):
        def canAttendMeetings(self, intervals):
            """
            :type intervals: List[Interval]
            :rtype: bool
            """
            intervals = sorted(intervals, key=lambda x: x.start)
            for i in xrange(len(intervals)):
                if i > 0 and intervals[i-1].end > intervals[i].start:
                    return False
            return True
            
            
**Solution #2: **

Want: in O(n) time on sorting
