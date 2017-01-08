## 246.Strobogrammatic Number

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Write a function to determine if a number is strobogrammatic. The number is represented as a string.

    For example, the numbers "69", "88", and "818" are all strobogrammatic.
    
**Solution:**

    def isStrobogrammatic(self, num):
        
        lookup = {'1': '1', '6': '9', '8': '8', '9': '6', '0': '0'}
        for i in xrange(len(num)/2+1):
            if num[i] not in lookup or lookup[num[i]] != num[~i]:
                return False
        return True