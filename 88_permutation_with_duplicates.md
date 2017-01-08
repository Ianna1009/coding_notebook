## 8.8 Permutation with Duplicates

Write a method to compute all permuations of a string whose characters are not necessarily unique. The list of permutations should not have duplicates.

**Idea:**

One simple way of handling this problem is to do the same work to check if a permutation has been created before and then, if not, add it to the list. A simple hash table will do the trick here. This solution will take O(n!) time in the worst case (and, in fact, in call cases).

While it's true we can't beat this worst case, we should be able to design an algorithm to beat this in many cases. Consider a string with all duplicate characters, like `aaaaaaaaaaaa`. This will take an extremely long time(since there are over 6 billion permutations of a 13-character string), even there is only one permutation.

We can start with computing the count of each letter(easy enough to get this -- just use a **hash  table**). For a string such as aabbbc, this would be:
    
    a -> 2, b -> 3, c -> 1

Let's generating a permutation of this string (now represented as a hash table). The first choice we make is whether to use an a, b or c as the first character. After that, we have a subproblem to solve: find all permutations the remaining characters, and append those to the already picked "prefix".

**Solution (Using Hash Table) New Idea!!!!:**

    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        frequency = collections.Counter(nums)
        self.printPerms(frequency, res, [], len(nums))
        return res
        
    def printPerms(self, h, res, tmp, n):
        # Base case: permutation has been completed.
        if n == 0:
            res.append([] + tmp)
            return
        
        for i in h:
            if h[i] > 0:
                h[i] -= 1
                self.printPerms(h, res, tmp + [i], n-1)
                h[i] += 1
                