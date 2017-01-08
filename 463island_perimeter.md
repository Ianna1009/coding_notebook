## 463.Island Perimeter

You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water. Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells). The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

**Example:**

    [[0,1,0,0],
     [1,1,1,0],
     [0,1,0,0],
     [1,1,0,0]]

    Answer: 16
    Explanation: The perimeter is the 16 yellow stripes in the image below:
![](island.png)

**Solution:**

    def islandPerimeter(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        if len(grid) == 0:
            return 0
        count = 0
        m, n = len(grid), len(grid[0])
        for i, row in enumerate(grid):
            for j, col in enumerate(row):
                if col == 1:
                    if j == 0 or row[j-1] == 0:
                        count += 1
                    if j == n-1 or row[j+1] == 0:
                        count += 1
                    if i == 0 or grid[i-1][j] == 0:
                        count += 1
                    if i == m-1 or grid[i+1][j] == 0:
                        count += 1
        return count