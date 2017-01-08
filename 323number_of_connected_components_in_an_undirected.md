## 323. Number of Connected Components in an Undirected Graph

Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.

**Example 1:**

         0          3
         |          |
         1 --- 2    4
    Given n = 5 and edges = [[0, 1], [1, 2], [3, 4]], return 2.

**Example 2:**

         0           4
         |           |
         1 --- 2 --- 3
    Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]], return 1.

**Note:**
You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges

**Solution #1 (Naive BFS):**

    def countComponents(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: int
        """
        adjList = [[] for _ in xrange(n)]
        for x, y in edges:
            adjList[x].append(y)
            adjList[y].append(x)
        visited = set()
        cont = 0
        queue = []
        for i in xrange(len(adjList)):
            if i not in visited:
                cont += 1
                queue.append(i)
                visited.add(i)
                while queue:
                    curr = queue.pop(0)
                    for node in adjList[curr]:
                        if node not in visited:
                            visited.add(node)
                            queue.append(node)
        return cont
                            
**Solution #2 **
        