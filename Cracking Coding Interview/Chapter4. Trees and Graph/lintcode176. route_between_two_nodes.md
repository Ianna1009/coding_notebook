## LintCode176. Route between two nodes

Given a directed graph, design an algorithm to find out whether there is a route between two nodes.

  Example

    Given graph:

    A----->B----->C
     \     |
      \    |
       \   |
        \  v
         ->D----->E
  for s = B and t = E, return true

  for s = D and t = C, return false
  
---
**Solution_1 BFS (Using queue):**

     class Directedgraph(object): 
         def __int__(self, x):
             self.label = x
             self.neighbors = []
             
    class Solution(object):   
        def hasRoute(self, graph, s, t):
            # write your code here
            if s == t:
                return True
            visited = set([s])
            queue = [s]
            while queue:
                curr = queue.pop(0)
                for ngb in curr.neighbors:
                    if ngb not in visited:
                        if ngb == t:
                            return True
                        queue.append(ngb)
                        visited.add(ngb)
            return False
            
** Solution_2 DFS(Recursive):
  
    class Solution:
        """
        @param graph: A list of Directed graph node
        @param s: the starting Directed graph node
        @param t: the terminal Directed graph node
        @return: a boolean value
        """
        def hasRoute(self, graph, s, t):
            # write your code here
            visited = set()
            return self.dfs(graph, s, t, visited)

        def dfs(self, graph, s, t, visited):
            if s == t:
                return True
            if s is None:
                return False
            visited.add(s)
            for ngb in s.neighbors:
                if ngb not in visited:
                    if self.dfs(graph, ngb, t, visited):
                        return True
            return False
          
          
 ** Note: **
 
 Every time you reach out to a new neighbor, you must mark it as visited to avoid cylic. 


            
               
