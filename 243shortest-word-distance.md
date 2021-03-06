## 243. Shortest Word Distance

Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

**For example,**

    Assume that words = ["practice", "makes", "perfect", "coding", "makes"].
    
    Given word1 = “coding”, word2 = “practice”, return 3.
    Given word1 = "makes", word2 = "coding", return 1.

**Note:**

You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.


**Naive Solution #1:**

    class Solution(object):
        def shortestDistance(self, words, word1, word2):
            """
            :type words: List[str]
            :type word1: str
            :type word2: str
            :rtype: int
            """
            MIN = len(words)
            distance = collections.defaultdict(list)
            for i, word in enumerate(words):
                distance[word].append(i)
            index1 = distance.get(word1)
            index2 = distance.get(word2)
            for i in index1:
                for j in index2:
                    MIN = min(MIN, abs(i-j))
            return MIN
        
**Note:**

This solution used hash table to store indices of words list. Thus it took O(n) space.
When getting the smallest difference, we need to iterate two lists, the worst case is both lists are half long of the words list, then it will be O((n/2)^2) time.

**Solution #2:**

Refer to solution in the discussion:
[https://discuss.leetcode.com/topic/22901/python-solution-o-n-time-o-1-space](https://discuss.leetcode.com/topic/22901/python-solution-o-n-time-o-1-space)
    
    class Solution(object):
        def shortestDistance(self, words, word1, word2):
            """
            :type words: List[str]
            :type word1: str
            :type word2: str
            :rtype: int
            """
            size = len(words)
            index1, index2 = size, size
            res = size
            
            for i in xrange(size):
                if words[i] == word1:
                    index1 = i
                    res = min(res, abs(index1-index2))
                elif words[i] == word2:
                    index2 = i
                    res = min(res, abs(index1-index2))
            return res

This will only take O(n) time and O(1) space.


