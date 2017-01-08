## Recursion
A good hint that a problem is recursive is that it can be built off of **sub-problems**.

When you hear a problem beginning with:

`` "Design am algorithm to compute the nth..."``

``Write code to list the first n ..."``

``Implement a method to compute all ..."``

Recursion it's often a good candidate.(Not always)

#### How to approach?

Many times, it will mean simply to compute ``f(n)`` by adding, removing something, or otherwise changing the solution for ``f(n-1)``.

Solutions: **Bottom-up** and **Top-down**.

  ** 1. Bottom-up(most intuitive)**
      
   Start with knowing how to solve the problem for a simple case, like:

            a list with only one element =>
            how to solve for 2 elments =>
            how to for 3 elements => ...
  The key here is to think about how to build the solution for one case off of the previous case.

  ** 2. Top-down(more complex)**

  Basically think about how to divide the problem for case N into sub-problems. ** Be careful of overlap between cases.**
  
#### Recursive vs. Iterative Solutions

** 1. Recursive: space inefficient. **

Each recursive call adds a new layer to  the stack, which means that if your algs has O(n) recursive calls, then it uses O(n) memory.

** 2. All recursive code can be implemented iteratively.** 

** *!!! Therefore before diving into recursive code, ask yourself how hard it would be implement it iteratively, and discuss the reads-offs with your interviewer.***

#### Problems from leetcode:
[226. Invert Binary Tree
](https://www.gitbook.com/book/ianna1009/leectcode-solution/edit#/edit/master/226.%20invert_binary_tree.md)





