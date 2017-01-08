## 289. Game of Life

According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

1. Any live cell with fewer than two live neighbors dies, as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population..
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

Write a function to compute the next state (after one update) of the board given its current state.

**Follow up: **

1. Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
2. In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

**Ideas:**

According to the game rules:

1. For 0: if count_1 == 3: become alive
2. For 1:
    * if count_1 < 2: become dead
    * if count_1 > 3: become dead
    * if count_1 == 2/3: continue
3. neighbors: dirs([-1,0,1,-1,1,-1,0,1], [-1,-1,-1,0,0,1,1,1])
  4. Using `becomeDead` and `becomeAlive` to keep record of changes.

**Naive Solution:**

    def gameOfLife(self, board):
        """
        :type board: List[List[int]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        m, n = len(board), len(board[0])
        becomeDead = set()
        becomeAlive = set()
        dirs = zip([1, 1, 1, 0, -1, -1, -1, 0], [0, 1, -1, -1, -1, 0, 1, 1])
        for i in xrange(m):
            for j in xrange(n):
                count = 0
                if board[i][j] == 0:
                    for r, c in dirs:
                        if 0 <= i+r < m and 0 <= j+c < n:
                            if board[i+r][j+c] == 1:
                                count += 1
                    if count == 3:
                        becomeAlive.add((i, j))
                if board[i][j] == 1:
                    for r, c in dirs:
                        if 0 <= i+r < m and 0 <= j+c < n:
                            if board[i+r][j+c] == 1:
                                count += 1
                    if count < 2:
                        becomeDead.add((i,j))
                    elif count > 3:
                        becomeDead.add((i,j))
        for r, c in becomeDead:
            board[r][c] = 0
        for r, c in becomeAlive:
            board[r][c] = 1
**Analysis:**

1. Although this solution works, but it's not space efficient, the worst case is O(MN) in space. We might think of a way to save space.
2. In the second follow-up, if the board is infinite in space, what should be improved?

**Answer:**

1. For saving space, since we've only got two status, we may only use two different numbers to denote updating status. -1 is becoming dead, 2 is becoming alive, that way we may also decide its current status in order to change its neighbors status.
2. If the board is infinitely large, it's impossible to iterate the whole board in finite time. What should we do?

**Solution #2 (In-place but slower)**

    def gameOfLife(self, board):
        """
        :type board: List[List[int]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        m, n = len(board), len(board[0])
        dirs = zip([1, 1, 1, 0, -1, -1, -1, 0], [0, 1, -1, -1, -1, 0, 1, 1])
        for i in xrange(m):
            for j in xrange(n):
                count = 0
                if board[i][j] == 0:
                    for r, c in dirs:
                        if 0 <= i+r < m and 0 <= j+c < n:
                            if board[i+r][j+c] == 1 or board[i+r][j+c] == -1:
                                count += 1
                    if count == 3:
                        board[i][j] = 2
                if board[i][j] == 1:
                    for r, c in dirs:
                        if 0 <= i+r < m and 0 <= j+c < n:
                            if board[i+r][j+c] == 1 or board[i+r][j+c] == -1:
                                count += 1
                    if count < 2 or count > 3:
                        board[i][j] = -1
        for i in xrange(m):
            for j in xrange(n):
                x = board[i][j]
                if x == -1:
                    board[i][j] = 0
                if x == 2:
                    board[i][j] = 1
                    
 **Solution of infinity board**
 
    def gameOfLife(self, board):
        """
        :type board: List[List[int]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        liveSet = set()
        for i in xrange(len(board)):
            for j in xrange(len(board[0])):
                if board[i][j] == 1:
                    liveSet.add((i,j))

        count = collections.Counter()
        for i, j in liveSet:
            for r in (i-1, i, i+1):
                for c in (j-1, j, j+1):
                    count[r,c] += 1
        
        newLiveSet = set()
        for i, j in count:
            if count[i,j] == 2 or count[i,j] == 3:
                newLiveSet.add((i,j))
        newLiveSet = liveSet
        return liveSet
            




            
                    
