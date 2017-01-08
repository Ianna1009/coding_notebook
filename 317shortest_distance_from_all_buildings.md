## 317.Shortest Distance from All Buildings

You want to build a house on an empty land which reaches all buildings in the shortest amount of distance. You can only move up, down, left and right. You are given a 2D grid of values 0, 1 or 2, where:

Each 0 marks an empty land which you can pass by freely.
Each 1 marks a building which you cannot pass through.
Each 2 marks an obstacle which you cannot pass through.
For example, given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2):

    1 - 0 - 2 - 0 - 1
    |   |   |   |   |
    0 - 0 - 0 - 0 - 0
    |   |   |   |   |
    0 - 0 - 1 - 0 - 0
The point (1,2) is an ideal empty land to build a house, as the total travel distance of 3+3+1=7 is minimal. So return 7.

**Note:**
There will be at least one building. If it is not possible to build such house according to the above rules, return -1.


**Solution #1 (Naive BFS): TLE**

    def shortestDistance(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m, n = len(grid), len(grid[0])
        dirs = zip([1,0,-1,0],[0,1,0,-1])
        MIN = float('inf')
        cont = self.getnumOfBuildings(grid)
        if cont == 0:
            return -1
        for i in xrange(m):
            for j in xrange(n):
                if grid[i][j] == 0:
                    visited = set((i, j))
                    total, v = 0, 0
                    queue = [(i, j, 0)]
                    while queue:
                        curr_i, curr_j, distance = queue.pop(0)
                        for x, y in dirs:
                            new_i, new_j = curr_i+x, curr_j+y
                            if 0 <= new_i < m and 0 <= new_j < n:
                                if (new_i, new_j) not in visited:
                                    if grid[new_i][new_j] == 1:
                                        total += distance + 1
                                        v += 1
                                    elif grid[new_i][new_j] == 2:
                                        continue
                                    else:
                                        queue.append((new_i, new_j, distance+1))
                                    visited.add((new_i, new_j))
                    MIN = min(MIN, total) if v == cont else MIN
        return MIN if MIN != float('inf') else -1
        
    def getnumOfBuildings(self, grid):
        count = 0
        m, n = len(grid), len(grid[0])
        for i in xrange(m):
            for j in xrange(n):
                if grid[i][j] == 1:
                    count += 1
        return count
        
**Analysis:**

While doing naive BFS, a couple of edge cases should be noticed:

* Every time you finish one round of searching, you need to keep record of total building you can reach at this empty spot, if you can't reach **all the buildings** from here, return -1. So you should firstly get the total # of buildings in the grid.
* Based on the first argument, if initially you got no buildings, return -1.
* You **can't pass through a BUILDING**!!!! Once you've reached one building, you should stop pushing this spot into queue cause you can't pass through it!
* Perhaps trying to start from buildings would make things easy!

**Solution #2 (Starting from Buildings and Doing BFS):**

    def shortestDistance(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m, n = len(grid), len(grid[0])
        dirs = zip([1,0,-1,0],[0,1,0,-1])
        total = [[[0,0] for _ in xrange(n)] for _ in xrange(m)]
        val = 0
        res = float('inf')
        for i in xrange(m):
            for j in xrange(n):
                if grid[i][j] == 1:
                    res = float('inf')
                    queue = [(i, j, 0)]
                    dist = [[0 for _ in xrange(n)] for _ in xrange(m)]
                    visited = set((i, j))
                    while queue:
                        curr_i, curr_j, distance = queue.pop(0)
                        for x, y in dirs:
                            new_i, new_j = curr_i+x, curr_j+y
                            if 0 <= new_i < m and 0 <= new_j < n:
                                if (new_i, new_j) not in visited and grid[new_i][new_j] == 0 and total[new_i][new_j][1] == val:
                                    dist[new_i][new_j] = distance+1
                                    total[new_i][new_j][0] += dist[new_i][new_j]
                                    total[new_i][new_j][1] += 1
                                    queue.append((new_i, new_j, distance+1))
                                    visited.add((new_i, new_j))
                                    res = min(res, total[new_i][new_j][0])
                    val += 1

        return res if res != float('inf') else -1
        
**Notes:**

1. `total` matrix has two functions: record total distance from all buildings and total number of reachable buildings. Thus check `total[new_i][new_j][1] == val` to make sure from this space you can reach all the buildings.
2. `queue` is to keep track of distance from this building (One specific building for one round). Not only `(new_i, new_j)` coordinates should be taken into consideration. Every time you need to update distance by taking more step`distance+1`. 
                                
                        
        




