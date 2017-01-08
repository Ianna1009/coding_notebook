## LC346. Moving Average from Data Stream

Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

**For example**,

    MovingAverage m = new MovingAverage(3);
    m.next(1) = 1
    m.next(10) = (1 + 10) / 2
    m.next(3) = (1 + 10 + 3) / 3
    m.next(5) = (10 + 3 + 5) / 3
    Show Company Tags
    Show Tags

---

** Solution: (Use queue)**

    class MovingAverage(object):

        def __init__(self, size):
            """
            Initialize your data structure here.
            :type size: int
            """
            self.cap = size
            self.queue = []
            self.total = 0

        def next(self, val):
            """
            :type val: int
            :rtype: float
            """
            self.total += val
            self.queue.append(val)
            n = len(self.queue)
            if n > self.cap:
                self.total -= self.queue[0]
                self.queue.pop(0)
            return float(self.total) / len(self.queue)


    # Your MovingAverage object will be instantiated and called as such:
    # obj = MovingAverage(size)
    # param_1 = obj.next(val)