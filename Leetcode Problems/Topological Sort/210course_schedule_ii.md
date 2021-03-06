## 210. Course Schedule II

There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

**For example:**

    2, [[1,0]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0. 

So the correct course order is [0,1]

    4, [[1,0],[2,0],[3,1],[3,2]]
There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. 

So one correct course order is [0,1,2,3]. Another correct ordering is[0,2,1,3].

**Solution #1 (Using degree list):**

    def findOrder(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: List[int]
        """
        res = []
        deg = {i: 0 for i in xrange(numCourses)}
        post = [[] for _ in xrange(numCourses)]
        
        for pair in prerequisites:
            deg[pair[1]] += 1
            post[pair[0]].append(pair[1])
        
        courses = set()
        while True:
            v = set()
            for c in deg:
                if deg[c] == 0:
                    res.append(c)
                    v.add(c)
                    for i in post[c]:
                        deg[i] -= 1
            if len(v) == 0:
                break
            for x in v:
                del deg[x]
        return res[::-1] if len(deg) == 0 else []