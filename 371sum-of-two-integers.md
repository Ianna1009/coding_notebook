## 371. Sum of Two integers

Calculate the sum of two integers a and b, but you are **not allowed **to use the operator`+`and`-`.

**Example:**  
    
    Given a= 1 and b= 2, return 3.

**Ideas:**

1. Using XOR(^) to get regular digits of sum (those digits where sum doesn't exceed 2)
2. Using bitwise and to get carry-on digits of sum (those digits where sum equals 2, however we got 1 instead, actually this 1 should be moved one digit to the left), thus move 1 bit to the left.

        For example:
              a = 2 (10)
            + b = 2 (10)
          -----------------
            SUM = 0 (00)
          carry = 3 (100) 
        
**Solution:**

    class Solution(object):
        def getSum(self, a, b):
            """
            :type a: int
            :type b: int
            :rtype: int
            """
            MAX = 0x7FFFFFFF
            mask = 0xFFFFFFFF
            if b == 0:
                return a if a <= MAX else ~ (a ^ mask)
            Sum = a ^ b
            carry = (a & b) << 1
            return self.getSum(Sum & mask, carry & mask)
            
**Notes:**

Need to take care of negative integers. Python doesn't use 8-bit numbers. It USED to use however many bits were native to your machine, but since that was non-portable, it has recently switched to using an INFINITE number of bits. 

According to [https://wiki.python.org/moin/BitwiseOperators ](https://wiki.python.org/moin/BitwiseOperators), -x is used by ~ (x-1). Therefore:

1. `mask` keeps the last 32 digits of an `int`
2. `MAX` makes sure the result is an `int`, if the length of result exceeds 32, which means it's probably a negative integer, then we convert it to correct negative representation. Using the above trick: `~ (x ^mask)`
