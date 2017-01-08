## 401.Binary Watch

A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59).

Each LED represents a zero or one, with the least significant bit on the right.


![](Binary_clock_samui_moon.jpg)

**For example, the above binary watch reads "3:25".**

Given a non-negative integer n which represents the number of LEDs that are currently on, return all possible times the watch could represent.

**Example:**

    Input: n = 1
    Return: ["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]
**Note:**

* The order of output does not matter.
* The hour must not contain a leading zero, for example "01:00" is not valid, it should be "1:00".
* The minute must be consist of two digits and may contain a leading zero, for example "10:2" is not valid, it should be "10:02".

**Solution:**

    def readBinaryWatch(self, num):
        """
        :type num: int
        :rtype: List[str]
        """
        tt = [1*64, 2*64, 4*64, 8*64, 32, 16, 8, 4, 2, 1]
        tpair = []
        self.getCombination(num, tt, [], tpair, 0)
        res = []
        for i in tpair:
            time = sum(i)
            hr, m = time / 64, time % 64
            if hr < 12 and m < 60:
                res.append('%d:%02d' %(hr, m))
        return res
        
    def getCombination(self, n, tt, tmp, res, pos):
        if len(tmp) == n:
            res.append([] + tmp)
            return
        for i in xrange(pos, len(tt)):
            self.getCombination(n, tt, tmp + [tt[i]], res, i+1)
                