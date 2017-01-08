## 249.Group Shifted Strings

Given a string, we can "shift" each of its letter to its successive letter, 

**for example:** 

    "abc" -> "bcd". 

We can keep "shifting" which forms the sequence:

    "abc" -> "bcd" -> ... -> "xyz"
Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.

**For example,** 

given: ["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"], 

      A solution is:

      [
        ["abc","bcd","xyz"],
        ["az","ba"],
        ["acef"],
        ["a","z"]
      ]
     
**Solution: **

    def groupStrings(self, strings):
        """
        :type strings: List[str]
        :rtype: List[List[str]]
        """
        hashTable = collections.defaultdict(list)
        for s in strings:
            if len(s) > 1:
                key = (len(s), (ord(s[1]) - ord(s[0]))%26)
                hashTable[key] += [s]
            else:
                hashTable["1"] += [s]
        return hashTable.values()
        