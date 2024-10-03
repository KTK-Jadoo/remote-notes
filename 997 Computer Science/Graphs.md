---
tags:
  - algorithms
  - compsci
date: 2024-10-01
source: "[[COMPSCI 170]]"
---

Nodes connected by edges.



Two kinds:
- Undirected (No direction, just connections) $G = (V, E)$
- Directed: One way (direction to each edge) $(u,v) \in E \text{ if } u\rightarrow v$

Parameters:
1) $n = |V| = \# \text{ of verticies}$
2) $m = |E| = \# \text{ of edges}$

$$m \lt n^2$$

# Representing Graphs


## Adjacency Matrix

An $n \times n$ matrix where the $i,j^\text{th}$ entry indicates if there is an edge between $i$ and $j$. $(0 \text{ or }1)$


## Adjacency List

A LinkedList of neighbors for every vertex. 

Out edges only for directed graph.



### Connectivity

#### DFS

Visited = [ ]