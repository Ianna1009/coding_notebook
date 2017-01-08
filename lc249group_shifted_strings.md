## LC249. Group Shifted Strings

Given a string, we can "shift" each of its letter to its successive letter, for example: "abc" -> "bcd". We can keep "shifting" which forms the sequence:

"abc" -> "bcd" -> ... -> "xyz"
Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.

    For example, given: ["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"], 
    
    A solution is:

      [
        ["abc","bcd","xyz"],
        ["az","ba"],
        ["acef"],
        ["a","z"]
      ]

___

** Solution: **

    class Solution(object):
        def groupStrings(self, strings):
            """
            :type strings: List[str]
            :rtype: List[List[str]]
            """
            hashTable = collections.defaultdict(list)
            for s in strings:
                key = tuple((ord(s[i]) - ord(s[0])) % 26 for i in xrange(len(s)))
                hashTable[key] += [s]
            return hashTable.values()
        