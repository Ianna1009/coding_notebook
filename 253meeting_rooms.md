## 253. Meeting Rooms

Given an array of meeting time intervals consisting of start and end times `[[s1,e1],[s2,e2],...] (si < ei)`, find the minimum number of conference rooms required.

For example,

    Given [[0, 30],[5, 10],[15, 20]],
    return 2.
    
**Tags** Heap, Greedy, Sort.

**Greedy** will be to take every interval one by one and find the number of intervals that overlap with it. Keep track of maximum number of intervals that overlap with an interval. Finally return the maximum value. Time Complexity of this solution is O(n2). Thus we won't use it.

---
**Solution #1: Sort Method (79 ms)**

    # Definition for an interval.
    # class Interval(object):
    #     def __init__(self, s=0, e=0):
    #         self.start = s
    #         self.end = e

    class Solution(object):
        def minMeetingRooms(self, intervals):
            """
            :type intervals: List[Interval]
            :rtype: int
            """
            t = [(x.start, 'start') for x in intervals]
            for x in intervals:
                t.append((x.end, 'end'))
            t.sort()
            MIN = 0
            startTotal, endTotal = 0, 0
            for i in t:
                if i[1] == 'start':
                    startTotal += 1
                else:
                    endTotal += 1
                MIN = max(MIN, startTotal - endTotal)
            return MIN
            
            
Reference: [Minimum Number of Platforms Required for a Railway/Bus Station](http://www.geeksforgeeks.org/minimum-number-platforms-required-railwaybus-station/). 
 
The ideas are the same. Time Complexity is O(n lg n) and Space Complexity is O(n), n is (# of intervals * 2).
 
**Solution #2: Heap ()** 

From tags, we see `heap` maybe another choice, but firstly guess it's gonna be O(n lg n) in time as well. 




 
 