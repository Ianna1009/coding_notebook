## 320.Generalized Abbreviation

Write a function to generate the generalized abbreviations of a word.

**Example:**

    Given word = "word", return the following list (order does not matter):
    ["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
    

**Ideas:**

**Solution:**

    def generateAbbreviations(self, word):
        """
        :type word: str
        :rtype: List[str]
        """
        res = []
        self.helper(word, res, "", 0)
        return res
    
    def helper(self, word, res, tmp, pos):
        if pos == len(word):
            res.append(tmp)
            return
        for i in xrange(pos, len(word)):
            abv = word[i]
            if i != pos:
                abv = str(i-pos) + word[i]
            self.helper(word, res, tmp + abv, i+1)
        res.append(tmp+str(len(word)-pos))
        
            