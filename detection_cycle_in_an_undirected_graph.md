## Detection Cycle in an Undirected Graph

Given an undirected graph, how to check if there is a cycle in the graph? For example, the following graph has a cycle 1-0-2-1.

    1 -- 0 -- 3
    |   /     |
    |  /      |
     2        4

Like directed graphs, we can use DFS to detect cycle in an undirected graph in O(V+E) time. 

We do a DFS traversal of the given graph. For every visited vertex `v`, if there is an adjacent `u` such that `u` is already visited and `u` is not parent of `v`, then there is a cycle in graph. If we don’t find such an adjacent for any vertex, we say that there is no cycle. The assumption of this approach is that there are no parallel edges between any two vertices.

**Application:**
1. Check if an undirected graph is a valid tree.
2. Topological sort.

**Algorithm:**

        # A recursive function that uses visited[] and parent to detect
        # cycle in subgraph reachable from vertex v.
        def isCyclicUtil(self,v,visited,parent):

            #Mark the current node as visited 
            visited[v]= True

            #Recur for all the vertices adjacent to this vertex
            for i in self.graph[v]:
                # If the node is not visited then recurse on it
                if  visited[i]==False : 
                    if(self.isCyclicUtil(i,visited,v)):
                        return True
                # If an adjacent vertex is visited and not parent of current vertex,
                # then there is a cycle
                elif  parent!=i:
                    return True

            return False


        #Returns true if the graph contains a cycle, else false.
        def isCyclic(self):
            # Mark all the vertices as not visited
            visited =[False]*(self.V)
            # Call the recursive helper function to detect cycle in different
            #DFS trees
            for i in range(self.V):
                if visited[i] ==False: #Don't recur for u if it is already visited
                    if(self.isCyclicUtil(i,visited,-1))== True:
                        return True

            return False
 