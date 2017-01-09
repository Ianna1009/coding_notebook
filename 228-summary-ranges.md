## 228. Summary Ranges

Given a sorted integer array without duplicates, return the summary of its ranges.

**For example**, given [0,1,2,4,5,7], return ["0->2","4->5","7"].

**Ideas:**

Intuitively, we can iterate through this given array, by using `left` and `right` to denote the left endpoint of the range and right for the right endpoint. 

Every time when the number got cut off, we update `left` and `right` with this number.
Every time when the number is consecutive with precious one, we only update `right` with this number.


**Solution:**
