## 399.Evaluate Division

Equations are given in the format A / B = k, where A and B are variables represented as strings, and k is a real number (floating point number). Given some queries, return the answers. If the answer does not exist, return -1.0.

Example:

    Given a / b = 2.0, b / c = 3.0. 
    queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ? . 
    return [6.0, 0.5, -1.0, 1.0, -1.0 ].

The input is: vector`<pair<string, string>> equations, vector<double>& values, vector<pair<string, string>> queries` , where `equations.size() == values.size()`, and the values are positive. This represents the equations. Return `vector<double>`.

According to the example above:

    equations = [ ["a", "b"], ["b", "c"] ],
    values = [2.0, 3.0],
    queries = [ ["a", "c"], ["b", "a"], ["a", "e"], ["a", "a"], ["x", "x"] ]. 

The input is always valid. You may assume that evaluating the queries will result in no division by zero and there is no contradiction.


**Solution #1:**

    import collections
    class Solution(object):
        def calcEquation(self, equations, values, queries):
            """
            :type equations: List[List[str]]
            :type values: List[float]
            :type queries: List[List[str]]
            :rtype: List[float]
            """
            # Construct a graph: once an equation is given, three edges should be added in the graph.
            eqs = collections.defaultdict(dict)
            for (x, y), i in zip(equations, values):
                eqs[x][y] = i * 1.0
                eqs[x][x], eqs[y][y] = 1.0, 1.0
                eqs[y][x] = 1.0 / i
            print eqs

            res = []
            # Try to use BFS to find a shortest equation path from x -> y:
            for i, (s, t) in enumerate(queries):
                visit = set()
                if s in eqs and s == t:
                    res.append(1.0)
                elif s in eqs and t in eqs:
                    queue = [[s,1.0]]
                    while queue:
                        x, div = queue.pop(0)
                        visit.add(x)
                        for node in eqs[x]:
                            if node not in visit:
                                newDiv = div*eqs[x][node]
                                if node == t:
                                    res.append(newDiv)
                                    break
                                else:
                                    queue.append([node, newDiv])
                    if len(res) == i:
                        res.append(-1.0)
                else:
                    res.append(-1.0)

            return res

