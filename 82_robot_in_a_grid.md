## 8.2 Robot in a Grid

Imagine a robot sitting on the upper left corner of grid with r rows and c columns. The robot can only move in two directions, right and down, but certain cells are "off limit" such that the robot cannot step on them. Design an algorithm to find a path for the robot from the top left to the bottom right.


**Solution #1 (Exponential TC):**

If we picture this grid, the only way to move to spot (r,c) is by moving to one of the adjacent spots: (r-1, c) or (r, c-1). So, we need to find a path to either (r-1, c) or (r, c-1).

How do we find a path to those spots? To find a path to (r-1,c) or (r, c-1), we need to move to one of its adjacent cells. So we need to find a path to a spot adjacent to (r-1, c), which are coordinates (r-2, c) and (r-1, c-1), or a spot adjacent to (r, c-1), which are (r-1, c-1) and (r, c-2). Observe that we list the point (r-1, c-1) twice; we'll discuss that issue later.

So then, to find a path from the origin, we just work **backwards** like this, **starting from the last cell**, we try to find a path to each of its adjacent cells. The recursive code below implements this algorithm.

    def getPath(self, maze):
        if len(maze) == 0 or len(maze[0]) == 0:
            return False
        path = []
        if self.pathFinder(maze, len(maze)-1, len(maze[0])-1, path):
            return path
        return None
        
    def pathFinder(self, maze, row, col, path):
        # if out of bounds or bot available, return.
        if col < 0 or row < 0 or not maze(row][col]:
            return False
        isAtOrigin = (row == 0) and (col == 0)
        if isAtOrigin or pathFinder(maze, row, col-1, path) or pathFinder(maze, row-1, col, path):
            path.append((row, col))
            return True
        return False
        
        
This solution is O(2^(r+c)), since each path has r+c steps and there are two choices we can make at each step. We should look for a faster way.

**Solution #2 (Polynomial TC Using memorization):**

If we walk through the algorithm, we'll see that we are visiting squares multiple times. In fact, we visit each square many, many times. After all, we have `rc` squares but we're doing O(2^(r+c)) work. If we were only visiting each square once, we would probably have an algorithm that was O(rc) (Unless we were somehow doing a lot of work during each visit).

How does our current algorithm work? To find a path to (r, c), we look for a path to an adjacent coordinate: (r-1, c) or (r, c-1). Of course, if one of those squares is off limits, we ignore it. Then we look at their adjacent coordinates: (r-2, c), (r-1, c-1), (r-1, c-1), and (r, c-2). The spot (r-1, c-1) appears twice, which means that we're duplicating effort. Ideally, we should remember that we already visited (r-1, c-1) so that we don't waste our time.

This is what the dynamic programming algorithm below does.

    def getPath(self, maze):
        if len(maze) == 0 or len(maze[0]) == 0:
            return None
        path = []
        failedPoints = set()
        if self.pathFinder(maze, len(maze), len(maze[0]), path, failedPoints):
            return path
        return None
        
    def pathFinde(self, maze, row, col, path, failedPoints):
        if col < 0 or row < 0 or not maze[row][col]:
            return False
        p = (row, col)
        if p in failedPoints:
            retuen False
        isAtOrigin = (row == 0) and (col == 0)
        if isAtOrigin or self.pathFinder(maze, row, col-1, path, failedPoints) or self.pathFinder(maze, row-1, col, path, failedPoints):
            path.append(p)
            return True
        failedPoints.append(p)
        return False
        
This simple change will make our run substantially faster. The algorithm will now take O(rc) time because we hit each cell just once.
    