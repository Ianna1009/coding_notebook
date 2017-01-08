## 1.6 String Compression

Implement a method to perform basic string compression using the counts of repeated characters. 

For example, the string `aabcccccaaa` would become `a2b1c5a3`. 

If the "compressed" string would not become smaller than the original string, your method should return the original string. You can assume the string has only uppercase and lowercase letters(a-z).

**Ideas:**

* Naive way would be iterate through the string. Copying characters to a new string and counting the repeats. At each iteration, check if the current character is the same as the next character. If not, add its compressed version to the result.

**Naive solution:**

    def compressBad(self, string):
        res = ""
        count = 0
        for i in xrange(len(string)):
            count += 1
            # if the next character is different than currest, append this char to result.
            if i + 1 > len(string) or string[i] != string[i+1]:
                res += string[i] + str(count)
                count = 0
        return res if len(res) < len(string) else string
        
**Anlysis on Naive Solution:**

* Runtime would be O(p + k^2), where p is the size of the original string and k is the number of character sequences. (If consider string concatenation is O(n^2) time when `res += string[i] + str(count)`, while Python wouldn't have this issue.)
* This solution create the compressed solution first and then return the shorter of the input string and the compressed string.
* When we don't have large number of repeating characters checking firstly will be more optimal.

---

**Optimal Solution:**

    def compress(string):
        # Check if final length and return input string if it would be larger.
        finalLength = self.countCompression(string)
        return string if finalLength >= len(String)
        
        count = 0
        res = ""
        for i in xrange(len(string)):
            count += 1
            if i + 1 >= len(string) or string[i] != string[i+1]:
                res += string[i] + str(count)
                count = 0
        return res
        
    def countCompression(self, string):
        compressedlength = 0
        count = 0
        for i in xrange(len(string)):
            count += 1
            if i + 1 >= len(string) or string[i] != string[i+1]:
                compressedLength += 1 + len(str(count))
                count = 0
        return compressedLength
        
**One other benefit of this solution is that we can initialize `StringBuilder` to its necessary capacity up-front**
