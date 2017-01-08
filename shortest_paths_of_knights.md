## Shortest Paths of Knights

Given a Source and Destination , find the minimum number of moves required to move a knight from Source to Destination in a 8 * 8 chess game.

---
** Solution: **

    class Solution(object):

        def __init__(self, size):
            self.size = size

        def shortestKnightPath(self, start, end):
            if start == end:
                return start
            ds = zip([1, 1, -1, -1, 2, 2, -2, -2], [2, -2, 2, -2, 1, -1, 1, -1])
            q = []
            visit = set()
            q.append((start, [start]))
            while q:
                curr = q.pop(0)
                if curr[0] == end:
                    return curr[1]
                pre_path = curr[1]
                row_ind, col_ind = curr[0][0], curr[0][1]
                for d in ds:
                    r, c = row_ind + d[0], col_ind + d[1]
                    if (r >= 0 and r < self.size) and (c >= 0 and c < self.size):
                        if (r, c) not in visit:
                            q.append(((r, c), pre_path + [(r, c)]))
                            visit.add((r, c))
                        else:
                            continue

            return None


