## 425.Word Squares

Given a set of words (without duplicates), find all word squares you can build from them.

A sequence of words forms a valid word square if the kth row and column read the exact same string, where 0 ≤ k < max(numRows, numColumns).

For example, the word sequence ["ball","area","lead","lady"] forms a word square because each word reads the same both horizontally and vertically.

    b a l l
    a r e a
    l e a d
    l a d y

**Note:**

* There are at least 1 and at most 1000 words.
* All words will have the exact same length.
* Word length is at least 1 and at most 5.
* Each word contains only lowercase English alphabet a-z.

**Example 1:**

    Input:
    ["area","lead","wall","lady","ball"]

    Output:
    [
      [ "wall",
        "area",
        "lead",
        "lady"
      ],
      [ "ball",
        "area",
        "lead",
        "lady"
      ]
    ]

    Explanation:
    The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).
**Example 2:**

    Input:
    ["abat","baba","atan","atal"]

    Output:
    [
      [ "baba",
        "abat",
        "baba",
        "atan"
      ],
      [ "baba",
        "abat",
        "baba",
        "atal"
      ]
    ]

    Explanation:
    The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).
    
**Solution:**

    def wordSquares(self, words):
        """
        :type words: List[str]
        :rtype: List[List[str]]
        """
        prefixTree = collections.defaultdict(set)
        for word in words:
            for i in xrange(len(word)):
                prefixTree[word[:i]].add(word)
        res = []
        self.helper(words, prefixTree, res, [])
        return res
    
    def helper(self, words, prefix, res, tmp):
        if len(tmp) == len(words[0]):
            res.append(tmp)
            return 
        candidates = self.validList(prefix, tmp)
        for word in candidates:
            self.helper(words, prefix, res, tmp + [word])
            
    def validList(self, d, tmp):
        level = len(tmp)
        prefix = ""
        for word in tmp:
            prefix += word[level]
        return d[prefix]