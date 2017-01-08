## Combination of Sets

Given a list of sets, choose one element from each set every time to form a new set, return all possible combinations. 

For example, given:

    {a, b, c}
    {1}
    {x, y}

    return:
    {a, 1, x}, {b, 1, x}, {c, 1, x}, {a, 1, y}, {b, 1, y}, {c, 1, y}

---
**Solution:**

    class Solution(object):

        def combinatioSets(self, sets):
            """
            :param sets: list(sets)
            :return: list(sets)
            """
            res = []
            self.dfs(sets, res, set(), 0)
            return res

        def dfs(self, sets, res, tmp, pos):

            if pos == len(sets):
                res.append(tmp.copy())
                return

            for i in sets[pos]:
                tmp.add(i)
                self.dfs(sets, res, tmp, pos+1)
                tmp.remove(i)