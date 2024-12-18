---
tags:
  - algorithms
  - compsci
date: 2024-10-01
source: "[[COMPSCI 170]]"
---
![[Pasted image 20241213191216.png]]
# Graph
Nodes connected by edges.

__Two kinds:__
- Undirected (No direction, just connections) $G = (V, E)$
- Directed: One way (direction to each edge) $(u,v) \in E \text{ if } u\rightarrow v$

__Parameters:__
1) $n = |V| = \# \text{ of verticies}$
2) $m = |E| = \# \text{ of edges}$
$$m \lt n^2$$
## Representing Graphs

### Adjacency Matrix
An $n \times n$ matrix where the $i,j^\text{th}$ entry indicates if there is an edge between $i$ and $j$. $(0 \text{ or }1)$

### Adjacency List
A LinkedList of neighbors for every vertex. Out edges only for directed graph.

![[Pasted image 20241213191346.png]]
For large sparse graphs, matrices take too much space. For large dense graphs, list get too long.

## Connectivity in Graphs

#### Key Questions

1. **Is there a path from $u$ to $v$?**
   - Determine if two vertices $u$ and $v$ are connected by any path in the graph.
2. **Is $G$ connected?**
   - Check if every pair of vertices in the graph is connected by some path, i.e., the graph is connected as a whole.
3. **What are the connected components?**
   - Identify all subsets of vertices such that:
     - Every pair of vertices within a subset is connected.
     - No vertex in one subset is connected to a vertex in another subset.

Connections can be tested by [[Depth First Search]].

