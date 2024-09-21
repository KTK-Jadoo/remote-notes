---
tags:
  - algorithms
date: 2024-09-20
source: "[[COMPSCI 170]]"
---
The divide-and-conquer strategy solves a problem by:
1. Breaking it into subproblems that are themselves smaller instances of the same type of problem
2. Recursively solving these subproblems
3. Appropriately combining their answers

The real work is done piecemeal, in three different places: in the partitioning of problems
into subproblems; at the very tail end of the recursion, when the subproblems are so small
that they are solved outright; and in the gluing together of partial answers. 

These are held together and coordinated by the algorithm’s core recursive structure.