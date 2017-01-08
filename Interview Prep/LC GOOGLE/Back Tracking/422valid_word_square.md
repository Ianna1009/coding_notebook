## 422.Valid Word Square

Given a sequence of words, check whether it forms a valid word square.

A sequence of words forms a valid word square if the kth row and column read the exact same string, where 0 ≤ k < max(numRows, numColumns).

**Note:**

* The number of words given is at least 1 and does not exceed 500.
* Word length will be at least 1 and does not exceed 500.
* Each word contains only lowercase English alphabet a-z.

**Example 1:**

    Input:
    [
      "abcd",
      "bnrt",
      "crmy",
      "dtye"
    ]

    Output:
    true

    Explanation:

      The first row and first column both read "abcd".
      The second row and second column both read "bnrt".
      The third row and third column both read "crmy".
      The fourth row and fourth column both read "dtye".
      Therefore, it is a valid word square.

**Example 2:**

    Input:
    [
      "abcd",
      "bnrt",
      "crm",
      "dt"
    ]

    Output:
    true

    Explanation:
    The first row and first column both read "abcd".
    The second row and second column both read "bnrt".
    The third row and third column both read "crm".
    The fourth row and fourth column both read "dt".

    Therefore, it is a valid word square.
**Example 3:**

    Input:
    [
      "ball",
      "area",
      "read",
      "lady"
    ]

    Output:
    false

    Explanation:
    The third row reads "read" while the third column reads "lead".

    Therefore, it is NOT a valid word square.
    
**Solution: **

    def validWordSquare(self, words):
        """
        :type words: List[str]
        :rtype: bool
        """
        m = len(words)
        n = len(words[0])
        if m != n:
            return False
        for r in xrange(m):
            # Get the length of rth word, valid if rth column is at the same length and each char is the same.
            curr_len = len(words[r])
            # Get the length of rth column:
            length = 0
            for i in xrange(m):
                if len(words[i]) > r:
                    length += 1
                else:
                    break
            if length != curr_len:
                return False
            for c in xrange(curr_len):
                if words[r][c] != words[c][r]:
                    return False
        return True
                   
        