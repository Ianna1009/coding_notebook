## 375. Guess Number Higher or Lower ii

We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number I picked is higher or lower.

However, when you guess a particular number x, and you guess wrong, you pay $x. You win the game when you guess the number I picked.

**Example:**

    n = 10, I pick 8.

    First round:  You guess 5, I tell you that it's higher. You pay $5.
    Second round: You guess 7, I tell you that it's higher. You pay $7.
    Third round:  You guess 9, I tell you that it's lower. You pay $9.
    
    Game over. 8 is the number I picked.
    
    You end up paying $5 + $7 + $9 = $21.
**Task:**

Given a particular n ≥ 1, find out how much money you need to have to guarantee a win.

**Hint:**

1. The best strategy to play the game is to minimize the maximum loss you could possibly face. Another strategy is to minimize the expected loss. Here, we are interested in the first scenario.
2. Take a small example (n = 3). What do you end up paying in the worst case?
3. Check out [this article ](https://en.wikipedia.org/wiki/Minimax)if you're still stuck.
4. The purely recursive implementation of minimax would be worthless for even a small n. You MUST use dynamic programming.
5. As a follow-up, how would you modify your code to solve the problem of minimizing the expected loss, instead of the worst-case loss?

**Ideas:**

Given hint #4, we can't solve it using Binary Search like [374. Guess Number Higher or Lower](https://github.com/Ianna1009/coding_notebook/blob/master/Interview%20Prep/LC%20GOOGLE/Binary%20Search/374guess_number_higher_or_lower.md), we need to find function for dynamic programming method.

`dp[i][j]` is the minimum cost of guessing between i and j.

**Solution:**

    class Solution(object):
        def getMoneyAmount(self, n):
            """
            :type n: int
            :rtype: int
            """
            dp = [[0 for _ in xrange(n+1)] for _ in xrange(n+1)]
            # dp[i][j] is the minimum cost when guessing between i and j
            # Both i and j range from 1..n
            for gap in xrange(1, n):
                for low in xrange(1, n+1-gap):
                    # low+gap < n+1
                    high = low + gap
                    dp[low][high] = min(x + max(dp[low][x-1], dp[x+1][high]) for x in xrange(low, high))
            return dp[1][n]