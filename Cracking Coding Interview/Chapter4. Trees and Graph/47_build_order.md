## 4.7 Build Order

You are given a list of projects and a list of dependencies (which is a list of pairs of objects, where the second project is dependent on the first project). All of a project's dependencies must be built before the project is. Find a build order that will allow the projects to be build. If there is no valid build order, return an error.

**Example:**

    Input:

    Projects: a, b, c, d, e, f
    Dependencies: (a, d), (f, b), (b, d), (f, a), (d, c)

    Output: f, e, a, b, d, c
    
**Solution #1: (Using in-coming degree and outgoing edges)**    

    def findOrder(self, projects, dependencies):
        # Construct Graph:
        degree = {i: 0 for i in xrange(len(projects))}
        orders = [[] for _ in xrange(len(projects))]
        for x, y in dependencies:
            degree[x] += 1
            orders[y].append(x)
        # Get order
        res = []
        while True:
            v = set()
            for i in degree:
                if degree[i] == 0:
                    v.add(i)
                    res.append(i)
                    offsprings = orders[i]
                    for x in offsprings:
                        degree[x] -= 1
            if len(v) == 0:
                break
            for x in v:
                del degree[x]
        return res if len(degree) == 0 else []
        
**Notes**
1. Need to check if all dependency edges are removed in order to quit loop.
2. Need to check if there are remaining nodes left in the graph to avoid infinity loop. (Cycalic Graph)
        
**Solution #2: (Using dfs)**



    

