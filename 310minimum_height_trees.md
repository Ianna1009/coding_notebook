## 310.Minimum Height Trees

For a undirected graph with tree characteristics, we can choose any node as the root. The result graph is then a rooted tree. Among all possible rooted trees, those with minimum height are called minimum height trees (MHTs). Given such a graph, write a function to find all the MHTs and return a list of their root labels.

**Format**

The graph contains n nodes which are labeled from 0 to n - 1. You will be given the number n and a list of undirected edges (each edge is a pair of labels).

You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

**Example 1:**

    Given n = 4, edges = [[1, 0], [1, 2], [1, 3]]

            0
            |
            1
           / \
          2   3
    return [1]

**Example 2:**

    Given n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]

         0  1  2
          \ | /
            3
            |
            4
            |
            5
    return [3, 4]
    
**Ideas:**

Through roughly thinking about construction of a tree:
1. If degree of a node is 1, then it can't be root unless the height of the tree is 1 given the definition of tree above. (no cycle means 1-degree node must exist)
2. If there exists any node whose degree is larger than 1, then it could be root, since it can reach to the 1-degree nodes.
3. Thus at most there will be n MHTs if there are n non-1-degree nodes in the graph. 

Therefore, we need to start to look at nodes that are non-1-degree. In order to do that, we need to construct a graph not only with adjacency list also the degree list. After that, we should think about using BFS to search for leaves to get minimal heights.

**Solution #1: Naive Way(TLE)**

    import collections
    class Solution(object):
        def findMinHeightTrees(self, n, edges):
            """
            :type n: int
            :type edges: List[List[int]]
            :rtype: List[int]
            """
            if len(edges) == 0:
                return [0]
            degree = collections.defaultdict(int)
            minHeight = float('inf')
            res = []
            # adjList = 0:[1,2,3], index means the number of node showing in the graph
            adjList = [[] for _ in xrange(n)]
            for x, y in edges:
                adjList[x].append(y)
                adjList[y].append(x)
                degree[x] += 1
                degree[y] += 1
            # From degree List, we may see how many possible roots we may have:
            for node in degree:
                if degree[node] > 1:
                    h = self.getHeight(adjList, degree, node)
                    if h < minHeight and res != []:
                        res.pop(0)
                    if h <= minHeight:
                        res.append(node)
                        minHeight = h
            return res if res != [] else degree.keys()

        def getHeight(self, graph, degree, x):
            height = 0
            queue = [(x, 0)]
            # Since each edge is undirected in this graph representation, we need to mark visited 
            visited = set([x])
            while queue:
                curr, cont = queue.pop(0)
                for node in graph[curr]:
                    if degree[node] > 1 and node not in visited:
                        queue.append((node, cont+1))
                        visited.add(node)
                height = max(height, cont+1)
            return height


                    
                    
                    
                    
**Solution #2**

        def findMinHeightTrees(self, n, edges):
            """
            :type n: int
            :type edges: List[List[int]]
            :rtype: List[int]
            """
            adjList = [[] for _ in xrange(n)]
            for x, y in edges:
                adjList[x].append(y)
                adjList[y].append(x)
            leaves = [x for x in xrange(n) if len(adjList[x]) <= 1]
            while n > 2:
                n -= len(leaves)
                newLeaves = []
                for x in leaves:
                    for y in adjList[x]:
                        adjList[y].remove(x)
                        if len(adjList[y]) == 1:
                            newLeaves.append(y)
                leaves = newLeaves
            return leaves

Reference: 

http://bookshadow.com/weblog/2015/11/26/leetcode-minimum-height-trees/
https://leetcode.com/discuss/71763/share-some-thoughts



