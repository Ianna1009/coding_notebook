## 8.7 Permutation w/o. Dups

Write a method to compute all permutations of a string of unique characters.

**Solution #1: Building from permutation of first n-1 characters.**

*Base Case:* Permutation of first character substring
The only permutation of `a1` is the string `a1`. So:

    P(a1) = a1

*Case: permutations of a1a2*

    P(a1a2) = a1a2 and a2a1

*Case: permutations of a1a2a3*

    P(a1a2a3) = a3a1a2, a1a3a2, a1a2a3, a3a2a1, a2a3a1, a2a1a3
    
*Case: permutations of a1a2a3a4*

This is the first interesting case. How can we generate permutation of a1a2a3a4 from a1a2a3?

Each permutation of a1a2a3a4 represents an ordering of a1a2a3. For example, a2a4a1a4 represents the order a2a1a3.

Therefore, if we took all the permutations of a1a2a3 and added a4 into all possible locations, we would get all permutations of a1a2a3a4.

    a1a2a3 -> a4a1a2a3, a1a4a2a3, a1a2a4a3, a1a2a3a4
    a1a3a2 -> a4a1a3a2, a1a4a3a2, a1a3a4a2, a1a3a2a4
    a3a1a2 -> a4a3a1a2, a3a4a1a2, a3a1a4a2, a3a1a2a4
    a3a2a1 -> a4a3a2a1, a3a4a2a1, a3a2a4a1, a3a2a1a4
    a1a3a2 -> a4a1a3a2, a1a4a3a2, a1a3a4a2, a1a3a2a4
    a2a3a1 -> a4a2a3a1, a2a4a3a1, a2a3a4a1, a2a3a1a4

We can now implement this algorithm recursively.

    def getPerms(self, string):
        if string is None:
            return None
        permutations = []
        # Base Case
        if len(string) == 0:
            permutations.append("")
        return permutations
        
        # Get the first char
        first = string[0]
        remainder = string[1:]
        words = self.getPerms(remaiders)
        for word in words:
            for j in xrange(len(word)):
                s = word[:j] + first + word[j:]
                permutations.append(s)
        return permutations
        
**Solution #2: Building from permutations of all n-1 character substrings.**

*Base Case:* Permutation of first character substring
The only permutation of `a1` is the string `a1`. So:

    P(a1) = a1

*Case: two-character strings:*
    
    P(a1a2) = a1a2 and a2a1,
    P(a2a3) = a2a3 and a3a2,
    P(a1a3) = a1a3 and a3a1.
    
*Case: three character strings:*

Here is where the cases get more interesting. Well, in essence, we just need to "try" each character as the first character and then append the permutations.

    P(a1a2a3) = {a1 + P(a2a3)} + (a2 + P(a1a3)} + {a3 + P(a1a2)}
    {a1 + P(a2a3)} -> a1a2a3, a1a3a2
    (a2 + P(a1a3)} -> a2a1a3, a2a3a1
    {a3 + P(a1a2)} -> a3a1a2, a3a2a1
  
Now that we can generate all permutations of three-character strings, we can use this to generate permutations of four-character strings.

    P(a1a2a3a4) = {a1 + P(a2a3a4)} + (a2 + P(a1a3a4)} + {a3 + P(a1a2a4)} + {a4 + P(a1a2a3)}

This is now a fairly straightforward algorithm to implement.

    def getPerms(self, string):
        res = []
        self.helper(string, res, "")
        return res
    
    def helper(self, remainder, res, prefix):
        if len(string) == 0:
            res.append(prefix)
        
        for i in xrange(len(remainder)):
            before = remainder[:i]
            after = remainder[i+1:]
            char = remainder[i]
            self.getPerms(before + after, res, before + char)
        
        
        