## 261.Graph Valid Tree

Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

**For example:**

    Given n = 5 and edges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.

    Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.

**Note:** 

you can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

**Ideas:**
1. "Determine a valid tree" means isolated node or two trees aren't allowed unless it's making up only a sigle-node tree.
2.  Detection of cycle in a graph: DFS.
3.  For DFS, in each recursion, visited nodes must be recorded. Thus using visited[[]] to keep in track.

**Solution #1 (DFS):**

    class Solution(object):
        def validTree(self, n, edges):
            """
            :type n: int
            :type edges: List[List[int]]
            :rtype: bool
            """
            # Construct graph:
            graph = [[] for _ in xrange(n)]
            for x, y in edges:
                graph[x].append(y)
                graph[y].append(x)
            #Detection of cycle using dfs
            visited = set()
            if not self.dfs(graph, 0, -1, visited):
                return False
            if len(visited) < n:
                return False
            return True

        def dfs(self, graph, v, parent, visited):
            if v in visited:
                return False
            visited.add(v)
            for node in graph[v]:
                if node != parent:
                    if not self.dfs(graph, node, v, visited):
                        return False
            return True

