## 8.5 Recursive Multiply

Write a recursive function to multiply two possible integers without using the * operator (or / operator). You can use addition, subtraction, and bit shifting, but you should minimize the number of those operations.

We can think about multiplying 8x7 as doing 8+8+8+8+8+8+8 (or adding 7 eight times). We can also think about it as the number of squares in an 8x7 grid.


**Solution #1:**

How would we count the number of squares in the grid? We could just count each cell. That's pretty slow, though.

Alternatively, we could count half the squares and then double it (by adding this count to itself). To count half the squares, we repeat the same process.

Of course this "doubling" only words if the number is in fact even. When it's not even, we need to do the counting/summing from scratch.

    def minProduct(a, b):
        bigger = [a, b][a < b]
        smaller = [a, b][a > b]
        return self.helper(smaller, bigger)
    
    def helper(self, smaller, bigger):
        if smaller == 0:
            return 0
        elif smaller == 1:
            return bigger
        
        # Compute half. If uneven, compute other half. If even, double it,
        s = smaller >> 1
        # Divide by 2
        side1 = self.helper(s, bigger)
        side2 = side1
        if smaller % 2 == 1:
            side2 = self.helper(smaller - s, bigger)
        return side1 + side2
        

**Solution #2:**

If we observe how the recursion operates, we'll notice that we have duplicate work. Consider this example:
    
    minProduct(17, 23)
        minProduct(8, 23)
            minProduct(4, 23) * 2
            ...
      + minProduct(9, 23)
            minProduct(4, 23)
            ...
          + minProduct(5, 23)
            ...
The second call to `minProduct(4, 23)` is unaware of the prior call, and so it repeats the same word. We should cache these results.


    def minProduct(a, b):
        bigger = [a, b][a < b]
        smaller = [a, b][a > b]
        memo = [None for _ in xrange(smaller+1)]
        return self.helper(smaller, bigger, memo)
    
    def helper(self, smaller, bigger, memo):
        if smaller == 0:
            return 0
        elif smaller == 1:
            return bigger
        elif memo[smaller] > 0:
            return memo[smaller]
        
        # Compute half. If uneven, compute other half. If even, double it,
        s = smaller >> 1
        # Divide by 2
        side1 = self.helper(s, bigger, memo)
        side2 = side1
        if smaller % 2 == 1:
            side2 = self.helper(smaller - s, bigger, memo)
        memo[smaller] = side1 + side2
        return memo[smaller]

**Solution #3:**

One thing we might notice when we look at this code is that a call to `minProduct` on an even number is much faster one on an odd number. For example, if we call `minProduct(30, 35)`, then we'll just do `minProduct(15, 35)` and double the result. However, if we do `minProduct(31, 35)`, then we'll need to call `minProduct(16, 35)`.

This is unnecessary, we can do:

`minProduct(31, 35) = 2 * minProduct(15, 35) + 35`

After all, since 31 = 2x15 + 1, then 31x35 = 2x15x35+35

The logic is:
**On even number, we just divide smaller by 2 and double the result of the recursive call. On odd numbers, we do the same, but then we also add bigger to this result.**
    
    def minProduct(a, b):
        bigger = [a, b][a < b]
        smaller = [a, b][a > b]
        return self.helper(smaller, bigger)
    
    def helper(self, smaller, bigger):
        if smaller == 0:
            return 0
        elif smaller == 1:
            return bigger
        
        s = smaller >> 1
        half = self.helper(s, bigger)
        if smaller % 2 == 1:
            return half + half + bigger
        else:
            return half + half        
        
        



