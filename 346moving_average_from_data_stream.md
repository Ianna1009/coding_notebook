## 346.Moving Average from Data Stream

Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

**For example,**

    MovingAverage m = new MovingAverage(3);
    m.next(1) = 1
    m.next(10) = (1 + 10) / 2
    m.next(3) = (1 + 10 + 3) / 3
    m.next(5) = (10 + 3 + 5) / 3

**Solution:**

    def __init__(self, size):
        """
        Initialize your data structure here.
        :type size: int
        """
        self.SUM = 0
        self.size = size
        self.queue = []

    def next(self, val):
        """
        :type val: int
        :rtype: float
        """
        size = self.size
        self.SUM += val
        self.queue.append(val)
        l = len(self.queue)
        if size < l:
            p = self.queue.pop(0)
            self.SUM -= p
            l -= 1
        return (self.SUM * 1.0) / l

    # Your MovingAverage object will be instantiated and called as such:
    # obj = MovingAverage(size)
    # param_1 = obj.next(val)
