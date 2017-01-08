## 8.12 Eight Queens (还没完）

Write an algorithm to print all ways of arranging eight queens on an 8x8 chess board so that none of them share the same row, column, or diagonal. In this case, "diagonal" means all diagonals, not just the two that bisect the board.


    class Solution(object):
        def solveNQueens(self, n):
            """
            :type n: int
            :rtype: List[List[str]]
            """
            res = []
            col = [['.' for _ in xrange(n)] for _ in xrange(n)]
            self.placeQueens(n, 0, col, res)
            return res

        def placeQueens(self, n, row, col, res):
            # Found valid placement (last row) 
            if row == n:
                res.append(["".join(x) for x in col])
            else:
                for j in xrange(n):
                    if self.checkValid(col, row, j):
                        # Place Queen
                        col[row][j] = 'Q'
                        self.placeQueens(n, row+1, col, res)
                        col[row][j] = '.'

        # Check if (r, c) is a valid spot to place a queen by checking if there is a queen in the same column or digonal. 
        def checkValid(self, columns, r, c):
            n = len(columns)
            for r2 in xrange(r):
                c2 = columns[r2][c]
                # Check if (r2, c2) invalidates (r, c) as a queen spot.
                # Check if rows have a queen in the same column.
                if c2 == 'Q':
                    return Fals
                # Check diagonal:
                rd = r - r2
                if c-rd >= 0 and columns[r2][c-rd] == "Q":
                    return False
                if c+rd <= n-1 and columns[r2][c+rd] == "Q":
                    return False
            return True


