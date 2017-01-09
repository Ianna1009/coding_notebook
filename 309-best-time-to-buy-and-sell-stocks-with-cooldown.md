## 309. Best Time to Buy and Sell Stock with Cooldown

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the **following restrictions:**

* You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
* After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)

**Example:**

    prices = [1, 2, 3, 0, 2]
    maxProfit = 3
    transactions = [buy, sell, cooldown, buy, sell]
**Ideas:**

With cooling-down after sell, at DAY i, we can:

1. Sell stock given we've bought this stock at Day i-1
2. Buy this stock only if we've sold this stock at Day i-2 (Day i-1 must be a cooling-down)
3. Do nothing if we can buy at Day i but we earned less if we didn't sell it at Day i-2. That means we need to compare profit at Day i-1 if we are holding the stock and Day i if we sold it at Day i-2 and buy it today.
Based on above thoughts, we can initialize two array to maintain our maximum coast and earn at Day i, naming them `buy` and `sell`, respectively. 

**Solution:**

    class Solution(object):
        def maxProfit(self, prices):
            """
            :type prices: List[int]
            :rtype: int
            """
            if not prices or len(prices) < 2:
                return 0
            n = len(prices)
            sell, buy = [0] * n, [0] * n
            buy[0] = -prices[0]
            buy[1] = max(buy[0], -prices[1])
            sell[1] = max(0, prices[1] - prices[0])
            
            for i in xrange(2, n):
                buy[i] = max(buy[i-1], sell[i-2]-prices[i])
                sell[i] = max(buy[i-1]+prices[i], sell[i-1])
                
            return sell[n-1]