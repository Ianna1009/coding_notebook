## LC425. Word Square

Given a set of words (without duplicates), find all word squares you can build from them.

A sequence of words forms a valid word square if the kth row and column read the exact same string, where 0 ≤ k < max(numRows, numColumns).

**For example,** 
the word sequence ["ball","area","lead","lady"] forms a word square because each word reads the same both horizontally and vertically.

    b a l l
    a r e a
    l e a d
    l a d y

**Note:**
There are at least 1 and at most 1000 words.
All words will have the exact same length.
Word length is at least 1 and at most 5.
Each word contains only lowercase English alphabet a-z.

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

** Analysis: **
(DFS + Pruning)
1. First need to construct a dictionary to store prefix of word
2. DFS method to ``search(word, line)``, word is the current word, line is the the row in the matrix
3. Use ``matrix`` to store words that has been chosen
4. ``prefix = matrix[0..line][line]`` if prefix doesn't exist, then pruning
5. Otherwise enumerate mdict [prefix], and recursively search.

---
** Solution:**


    class Solution(object):
        def wordSquares(self, words):
            """
            :type words: List[str]
            :rtype: List[List[str]]
            """
            m = len(words)
            n = len(words[0])
            mdict = collections.defaultdict(set)
            for word in words:
                for i in xrange(n):
                    mdict[word[:i]].add(word)
            matrix = []
            ans = []
            def search(word, line):
                matrix.append(word)
                if line == n:
                    ans.append(matrix[:])
                else:
                    prefix = ''.join(matrix[x][line] for x in xrange(line))
                    for word in mdict[prefix]:
                        search(word, line+1)
                matrix.pop()
            for word in words:
                search(word, 1)
            return ans
            
Solution Reference:
[http://bookshadow.com/weblog/2016/10/16/leetcode-word-squares/](http://bookshadow.com/weblog/2016/10/16/leetcode-word-squares/)