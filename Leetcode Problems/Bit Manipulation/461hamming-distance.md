## 461. Hamming Distance

The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.

Given two integers `x`and  `y`, calculate the Hamming distance.

**Note:**  
0 ≤`x`, `y`&lt; 231.

**Example:**

```
Input:
 x = 1, y = 4


Output:
 2


Explanation:

1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

The above arrows point to positions where the corresponding bits are different.
```

**Ideas:**

Upon observation, we can see the method of counting in the result is the same as the bit operation: ^.

^ of the same values: return 0

^ of diff values: return 1

Thus we can think of using x^y to get the counts of distinct positions in corresponding bits.

** Solution: **

```
class Solution(object):
    def hammingDistance(self, x, y):
        """
        :type x: int
        :type y: int
        :rtype: int
        """
        return bin(x ^ y).count("1")
```



