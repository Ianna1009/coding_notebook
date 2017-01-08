## 447.Number of Boomerangs

Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points (i, j, k) such that the distance between i and j equals the distance between i and k (**the order of the tuple matters**).

Find the number of boomerangs. You may assume that n will be at most 500 and coordinates of points are all in the range [-10000, 10000] (inclusive).

**Example:**

    Input:
    [[0,0],[1,0],[2,0]]

    Output:
    2

    Explanation:
    The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]


**Ideas:**

Given a point as the first point i, in order to get a boomerang, we need to compute distances of other points to it and then find two points that have the same distance. 

In order to record distanced of other points to point i, we may need Hash Table.

**Solution:**

    def numberOfBoomerangs(self, points):
    
        res = 0
        for x1, y1 in points:
            d = collections.defaultdict(int)
            for x2, y2 in points:
                dis = (x1-x2)*(x1-x2) + (y1-y2)*(y1-y2)
                d[dis] += 1
            for i in d:
                res += d[i] * (d[i] - 1)
        return res
