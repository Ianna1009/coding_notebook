## LC77. Combinations

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:

    [
      [2,4],
      [3,4],
      [2,3],
      [1,2],
      [1,3],
      [1,4],
    ]
    
 ---
 **Solution:**
 
     class Solution(object):
        def combine(self, n, k):
            ans = []
            self.dfs(n, k, ans, [], 1)
            return ans

        def dfs(self, n, k, res, tmp, pos):
            if len(tmp) == k:
                res.append([]+tmp)
                return
            for i in xrange(pos, n+1):
                if n+1-pos < k-len(tmp):
                    return
                tmp.append(i)
                self.dfs(n, k, res, tmp, i+1)
                tmp.pop()


            