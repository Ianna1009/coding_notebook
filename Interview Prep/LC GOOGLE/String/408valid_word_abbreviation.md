## 408.Valid Word Abbreviation

Given a non-empty string s and an abbreviation abbr, return whether the string matches with the given abbreviation.

A string such as "word" contains only the following valid abbreviations:

    ["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
Notice that only the above abbreviations are valid abbreviations of the string "word". Any other string is not a valid abbreviation of "word".

**Note:**

Assume s contains only lowercase letters and abbr contains only lowercase letters and digits.

**Example 1:**

    Given s = "internationalization", abbr = "i12iz4n":

    Return true.
**Example 2:**

    Given s = "apple", abbr = "a2e":

    Return false.
    
    
**Solution:**

    def validWordAbbreviation(self, word, abbr):
        """
        :type word: str
        :type abbr: str
        :rtype: bool
        """
        i, j = 0, 0
        m, n = len(abbr), len(word)
        while i < m and j < n:
            if '0' <= abbr[i] <= '9':
                if abbr[i] == '0':
                    return False
                cont = 0
                while i < m and '0' <= abbr[i] <= '9':
                    cont *= 10
                    cont += int(abbr[i])
                    i += 1
                j += cont
            else:
                if abbr[i] != word[j]:
                    return False
                i += 1
                j += 1
        return i == m and j == n
            
            
        
        