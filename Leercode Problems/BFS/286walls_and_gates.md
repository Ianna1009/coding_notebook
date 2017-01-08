## 286.Walls and Gates

You are given a m x n 2D grid initialized with these three possible values.

    -1 - A wall or an obstacle.
    0 - A gate.
    INF - Infinity means an empty room. 

We use the value 231 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.
Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.

For example, given the 2D grid:

    INF  -1  0  INF
    INF INF INF  -1
    INF  -1 INF  -1
      0  -1 INF INF
After running your function, the 2D grid should be:

      3  -1   0   1
      2   2   1  -1
      1  -1   2  -1
      0  -1   3   4
      
**Solution #1 (Naive BFS for searching Using queue): TLE**
class Solution(object):
    
    def wallsAndGates(self, rooms):
        """
        :type rooms: List[List[int]]
        :rtype: void Do not return anything, modify rooms in-place instead.
        """
        if len(rooms) == 0:
            return
        INF = 2147483647
        m, n = len(rooms), len(rooms[0])
        for i in xrange(m):
            for j in xrange(n):
                if rooms[i][j] == INF:
                    rooms[i][j] = self.findGate(rooms, i, j, m, n)
        
    def findGate(self, rooms, x, y, m, n):
        INF = 2147483647
        dummy = (-1, -1)
        queue = [(x, y), dummy]
        visited = set((x, y))
        cont = 1
        dirs = zip([1, 0, -1, 0], [0, 1, 0, -1])
        while queue:
            curr_x, curr_y = queue.pop(0)
            if (curr_x, curr_y) == dummy:
                cont += 1
                if queue == []:
                    return INF
                queue.append(dummy)
                continue
            for d in dirs:
                new_x, new_y = curr_x + d[0], curr_y + d[1]
                if new_x < 0 or new_x > m-1 or new_y < 0 or new_y > n-1:
                    continue
                if rooms[new_x][new_y] == -1:
                    continue
                elif rooms[new_x][new_y] == 0:
                    return cont
                elif (new_x, new_y) not in visited:
                    visited.add((curr_x,curr_y))
                    queue.append((new_x, new_y))
                    
**Ideas:**
1. The reason I think of timing out is thw two loops in the first part. We've been doing repeatedly searching for gates in the part a lot. Perhaps we can do a little better.
2. Using the other departure option: starting from the gate and searching for rooms.

**Solution #2: Starting from gates using BFS**
    
    def wallsAndGates(self, rooms):
        """
        :type rooms: List[List[int]]
        :rtype: void Do not return anything, modify rooms in-place instead.
        """
        if len(rooms) == 0:
            return
        m, n = len(rooms), len(rooms[0])
        queue = []
        dirs = zip([1, 0, -1, 0], [0, 1, 0, -1]）
        for i in xrange(m):
            for j in xrange(n):
                if rooms[i][j] == 0:
                    queue.append((i,j))
        while queue:
            curr_x, curr_y = queue.pop(0)
            for d in dirs:
                new_x, new_y = curr_x + d[0], curr_y + d[1]
                if new_x < 0 or new_x > m-1 or new_y < 0 or new_y > n-1 or rooms[new_x][new_y] < rooms[curr_x][curr_y] + 1:
                    continue
                rooms[new_x][new_y] = rooms[curr_x][curr_y] + 1
                queue.append((new_x, new_y))
                

**Note:**
1. While searching, every time coming across a new grid, if it's out of the bounds or the new distance is smaller than (distance of the previous room + 1), then continue
2. Other than that, we fill the new distance into the new room and append this new coordinates into queue.
3. After we pop out all elements in queue, we finish searching the whole matrix.


                
