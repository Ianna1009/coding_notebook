## 1.3 URLify

Write a method to replace all spaces in a string with '%20'. You may assume that the string has sufficient space at the end to hold the additional characters, and that you are given the "true" length of the string. (Note: if implementing in java, please use a character array so that you can perform this operation in place.)

**Example:**

    input:  "Mr John Smith    ", 13
    output: "Mr%20John%20Smith"
    
**Solution: **

    def replaceSpaces(self, str, length):
            """
            strType: list[str]
            """
            count = 0
            for i in xrange(length):
                if str[i] == ' ':
                    count += 1
            # the number of spaces is count, length - count: # of chars 
            index = length + count*2 + (length-count)
            for i in xrange(length, 0, -1):
                if str[i] == " ":
                    str[index-1] = "0"
                    str[index-2] = "2"
                    str[index-3] = "%"
                    index -= 3
                else:
                    str[index-1]   = str[i]
                    index -= 1
                    
        