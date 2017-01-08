## 332.Reconstruct Itinerary

Given a list of airline tickets represented by pairs of departure and arrival airports [from, to], reconstruct the itinerary in order. All of the tickets belong to a man who departs from JFK. Thus, the itinerary must begin with JFK.

Note:
1. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].
2. All airports are represented by three capital letters (IATA code).
3. You may assume all tickets form at least one valid itinerary.

Example 1:

    tickets = [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
    Return ["JFK", "MUC", "LHR", "SFO", "SJC"].
Example 2:

    tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
    Return ["JFK","ATL","JFK","SFO","ATL","SFO"].
    Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"]. But it is larger in lexical order.
    
**Ideas:**
1. According to the problem, return list starts from 'JFK'.
2. `tickets` is edge list of the graph.
3. `node.decendants()` should be sorted.

**Solution #1:**

    import collections
    class Solution(object):
        def findItinerary(self, tickets):
            """
            :type tickets: List[List[str]]
            :rtype: List[str]
            """
            trips = collections.defaultdict(dict)
            for dep, arr in tickets:
                trips[dep].setdefault(arr, 0)
                # Some trips happen several times
                trips[dep][arr] += 1
            res = ['JFK']
            self.dfs(trips, len(tickets)+1, 'JFK', res)
            return res

        def dfs(self, trips, m, start, res):
            if len(res) == m:
                return True
            if start in trips:
                for end, cnt in sorted(trips[start].items()):
                    if cnt != 0:
                        res += [end]
                        trips[start][end] -= 1
                        if self.dfs(trips, m, end, res):
                            return True
                        trips[start][end] += 1
                        del res[-1]
            return False

                
**Solution #2:**

    class Solution(object):
        def findItinerary(self, tickets):
            """
            :type tickets: List[List[str]]
            :rtype: List[str]
            """
            targets = collections.defaultdict(list)
            for a, b in sorted(tickets)[::-1]:
                targets[a] += b,
            route = []
            def visit(airport):
                while targets[airport]:
                    visit(targets[airport].pop())
                route.append(airport)
            visit('JFK')
            return route[::-1]
            
 Refer to [风影博客](http://bookshadow.com/weblog/2016/02/05/leetcode-reconstruct-itinerary/)