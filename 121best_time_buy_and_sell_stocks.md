## 121.Best Time Buy and Sell Stocks

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Example 1:

    Input: [7, 1, 5, 3, 6, 4]
    Output: 5

    max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
Example 2:

    Input: [7, 6, 4, 3, 1]
    Output: 0

    In this case, no transaction is done, i.e. max profit = 0.

**Solution: (Naive)**

    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        p = 0
        for i in xrange(1, len(prices)):
            profit = 0
            for j in xrange(i):
                profit = max(profit, (prices[i] - prices[j]))
            p = max(p, profit)
        return p
            
**Solution: (Memorization)**

    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        s_time = 0
        b_time = 0
        p = 0
        for i in xrange(1, len(prices)):
            if prices[i] < prices[b_time]:
                b_time = i
            profit = prices[i] - prices[b_time]
            if profit > p:
                s_time = i
                p = max(p, profit)
        return p