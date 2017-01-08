## 444. Sequence Reconstruction

Check whether the original sequence org can be uniquely reconstructed from the sequences in seqs. The org sequence is a permutation of the integers from 1 to n, with 1 ≤ n ≤ 104. Reconstruction means building a shortest common supersequence of the sequences in seqs (i.e., a shortest sequence so that all sequences in seqs are subsequences of it). Determine whether there is only one sequence that can be reconstructed from seqs and it is the org sequence.

Example 1:

    Input:
    org: [1,2,3], seqs: [[1,2],[1,3]]

    Output:
    false

    Explanation:

    [1,2,3] is not the only one sequence that can be reconstructed, because [1,3,2] is also a valid sequence that can be reconstructed.

Example 2:

    Input:
    org: [1,2,3], seqs: [[1,2]]

    Output:
    false

    Explanation:
    The reconstructed sequence can only be [1,2].
Example 3:

    Input:
    org: [1,2,3], seqs: [[1,2],[1,3],[2,3]]

    Output:
    true

    Explanation:
    The sequences [1,2], [1,3], and [2,3] can uniquely reconstruct the original sequence [1,2,3].
Example 4:

    Input:
    org: [4,1,5,2,6,3], seqs: [[5,2,6,3],[4,1,5,2]]

    Output:
    true

**Idea:**
1. Using `deg` as outgoing degree dict of the graph
2. Using `adjList` as adjacency list of ancestors in the graph.
3. Be careful of `seqs=[]`.


** Analysis: **

Once the directed graph has been constructed, we need to check if `org` is in the same order as how the graph is flowing through.
  1. If org[i] can't get to org[i+1] in the graph, return False
  2. If i holds, remove edge(org[i], org[i-1]) from the graph, eventually if the last node in org has any out-going degree(i.e. `deg[len(org)-1] != 0`), return False
  3. If integer in `seqs` didn't appear in `org`, like: `org=[1], seqs=[[1000,0],[-1,1]]`: return False.

Then the code will be:

    class Solution(object):
        def sequenceReconstruction(self, org, seqs):
            """
            :type org: List[int]
            :type seqs: List[List[int]]
            :rtype: bool
            """
            # Build a graph from seqs:
            m = len(org)
            adjList = [set() for _ in xrange(m)]
            deg = {i: 0 for i in xrange(1, m+1)}
            # One edge case to consider: org = [1] but seqs = []
            if not seqs:
                return False
            for group in seqs:
                n = len(group)
                for i in xrange(n):
                    # if number in seqs not in org: org = [1], seqs = [[100000], [1, 9], [-1, 0]]
                    if group[i] > m or group[i] <= 0:
                        return False
                    if i > 0:
                        if group[i-1] not in adjList[group[i]-1]:
                            deg[group[i-1]] += 1
                            adjList[group[i]-1].add(group[i-1])
            for i in xrange(m):
                prev = org[i]
                if i < m-1:
                    dec = org[i+1]
                    if len(adjList[dec-1]) != 0 and prev in adjList[dec-1]:
                        deg[prev] -= 1
                    elif prev not in adjList[dec-1]:
                        return False
                if i == m-1:
                    return deg[prev] == 0


                
            
