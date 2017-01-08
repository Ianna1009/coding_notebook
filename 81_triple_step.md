## 8.1 Triple Step

A child is running up a staircase with n steps and can hop wither 1 step, 2 steps, or 3 steps at a time. Implement a method to count how many possible ways the child can run up the stairs.

**Ideas:**

How many ways are there to get to the nth step? We can relate it to some **sub-problems.**

    T(n) = T(n-1) + T(n-1) + T(n-2)
    
**Solution #1 (Brute Force):**

The one tricky bit is defining the base case. If we have 0 steps to go (we're currently standing on the step) are there zero paths to that step or one path?

T(0) = 1 ? 0

You could define it either way. There is no "right" answer here. However it's a lot easier to define it as 1. If you defined it as 0, then you need also define T(1) = 1, T(2) = 1 and T(3) = 1.

    def countSteps(self, n):
        if n < 0:
            return 0
        elif n == 0:
            return 1
        else:
            return countSteps(n-1) + countSteps(n-2) + countSteps(n-3)
            
This algorithm is exponential(roughly O(3^n)) since each call branches out to three more calls.
            
**Solution #2 (Memorization Solution):**
 
The previous solution for `countSteps` is called many times for the same values, which is unnecessary. We can fix this through memorization.
Essentially, if we've seen this value of n before, return the caches value. Each time we computes a fresh values, add it to the caches.

Typically we use a `HashMap<integer, integer>` for a cache. In this case, the keys will be exactly 1 through n. It's more compact to use an **integer array**.

    def counSteps(self, n):
        memo = [None for _ in xrange(n+1)]
        return self.count(n, memo)
    
    def count(self, n, memo):
        if n < 0:
            return 0
        elif n == 0:
            return 1
        else:
            memo[n] = self.count(n-1, memo) + self.count(n-2, memo) + self.count(n-3, memo)
        return memo[n]
        
Regardless of whether or not you use memorization, note that the number of ways will quickly overflow the bounds of an integer. By the time you get to just n = 37, the result has already overflowed. Using a long will delay, but not completely solve, this issue.

It is great to communicate this issue with your interviewer. He probably won't ask you to work around it**(Although you could, with a `BigInteger` class)**, but it's nice to demonstrate that you think about these issues.

