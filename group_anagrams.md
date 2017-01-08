## 10.2/LC49. Group Anagrams

Write a method to sort an array of strings so that all the anagrams are next to each other.

    For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 
    Return:

    [
      ["ate", "eat","tea"],
      ["nat","tan"],
      ["bat"]
    ]
    
Note: All inputs will be in lower-case.


**Idea:**

This problem asks us to group the strings in an array such that the anagrams appear next to each other. Note that no specific ordering of the words is required, other than this.

We need a quick and easy way of determining if two strings are anagrams of each other. What defines if two words are anagrams of each other? Well, anagrams are words that have the same characters but in different orders. It follows then that if we can put the characters in the same order, we can easily check if the new words are identical.

One way to do this is to just apply any standard sorting algorithm, like merge sort or quick sort, and modify the comparator. This comparator will be used to indicate that two strings are anagrams of each other are equivalent.

What's the easiest way of checking if two words are anagrams? We could count the occurrences of the distinct characters in each string and return true if they match. Or, we could just sort the string. After all, two words which are anagrams will look the same once they're sorted.

**Attempt #1 (TLE):**

    class Solution(object):
        def groupAnagrams(self, strs):
            """
            :type strs: List[str]
            :rtype: List[List[str]]
            """
            res = []
            visit = set()
            for i in xrange(len(strs)):
                if i not in visit:
                    res.append([strs[i]]) 
                for j in xrange(i+1, len(strs)):
                    if self.compare(strs[i], strs[j]):
                        if j not in visit:
                            visit.add(j)
                            res[-1].append(strs[j])
            return res

        # Using naive way to sort each word and compare them to see if they are the same.
        def compare(self, s1, s2):
            def sortchars(strs):
                strs = sorted(strs)
                return strs
            return sortchars(s1) == sortchars(s2)
            
This `compare` method will take O(n lg n) time. And the main group method will take O(n^2) time and O(n) space.

This may be the best we can do for a general sorting algorithm, but we don't actually need to fully sort the array. We only need to group the strings in the array by anagram.

We can do this by using a **hash table** which maps from the **sorted version of a word** to **a list of its anagrams**. So, for example, `acre` will map to the list `{acre, race, care}`. 

** Solution #2 (hash table):**

    import collections
    
    class Solution(object):
        def groupAnagrams(self, strs):
            """
            :type strs: List[str]
            :rtype: List[List[str]]
            """
            if len(strs) < 2:
                return [strs]
            h = collections.defaultdict(list)
            for s in strs:
                key = "".join(sorted(s))
                h[key].append(s)

            res = [h[x] for x in h]  
            return res
            
