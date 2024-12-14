---
tags:
  - algorithms
date: 2024-12-13
source: "[[COMPSCI 170]]"
---
# Depth First Search (DFS)

## Algorithm Description

1. **Initialization**:
   - For each vertex $u \in V$, set `visited[u] = FALSE`.

2. **Explore Function**:
   - When a vertex $v$ is visited, perform the following steps:
     - Set `visited[v] = TRUE`.
     - For each edge $(v, w) \in E$:
       - If `visited[w] = FALSE`, recursively call `EXPLORE(w)`.

```java
EXPLORE(vertex v):
	visited[v] = TRUE
	for each edge (v, w) ∈ E:
		if NOT visited[w]:
		EXPLORE(w)

DFS(Graph G):
	visited[u] = FALSE for all u ∈ V
	for each vertex v ∈ V:
		if NOT visited[v]:
		EXPLORE(v)
```

---

#### Key Observations

- DFS explores as far as possible along each branch before backtracking.
- It can be used to:
  1. Check [[Graphs#Connectivity in Graphs|connectivity]] between two vertices.
  2. Find all connected components in a graph.
  3. Detect cycles in a graph.

_Runtime:_ $O(V + E)$ where $V$ is the number of vertices and $E$ is the number of edges.

### Property of `EXPLORE(u)`

**Statement**:  
`EXPLORE(u)` visits exactly the vertices $v$ such that the graph $G$ has a path from $u$ to $v$.

#### Proof:
1. **If a vertex $v$ is visited by `EXPLORE(u)`, then there is a path from $u$ to $v$.**

   - `EXPLORE(u)` only visits a vertex $v$ if it recursively follows edges starting from $u$.  
   - Each recursive call corresponds to traversing an edge, so if $v$ is visited, there exists a sequence of edges forming a path from $u$ to $v$.

2. **If there is a path from $u$ to $v$, then `EXPLORE(u)` visits $v$.**
   - Suppose not. Assume there is a path $P$ from $u$ to $v$, but `EXPLORE(u)` does not visit $v$.
   - Let $w_k$ be the first vertex along the path $P$ that is **not visited** by `EXPLORE(u)`.
     - Clearly, $w_{k-1}$ (the vertex preceding $w_k$ along $P$) **is visited**, since it comes earlier along the path.
   - Since $(w_{k-1}, w_k)$ is an edge in $G$, and `EXPLORE(w_{k-1})` is called, it would recursively call `EXPLORE(w_k)`.  
     - This contradicts the assumption that $w_k$ is not visited.

#### Conclusion:
Since both directions of the implication hold, we conclude that `EXPLORE(u)` visits **exactly** the vertices $v$ such that there is a path from $u$ to v.


---

#### Runtime of DFS

1. **Key Observations**:
   - `EXPLORE(v)` is called **once per vertex**.
   - Processing each vertex involves:
     - Marking it visited: $O(1)$.
     - Iterating over its neighbors: $O(\text{deg}(v))$.

2. **Total Runtime**:
   - Summing over all vertices:
     $$
     \text{Total Runtime} = \sum_{v} O(1 + \text{deg}(v)) = O(n + m)
     $$
   - Where $n = |V|$ (number of vertices) and $m = |E|$ (number of edges).

## DFS in Directed Graphs

#### Additional Features of DFS in Directed Graphs
1. **Pre- and Post-Visit Times**:
   - Each vertex $v$ is assigned a **pre-visit** time when it is first discovered.
   - A **post-visit** time is recorded after all its neighbors have been explored.

2. **Edge Classification**:
   - During DFS, edges in a directed graph are classified as:
     - **Tree edges**: Part of the DFS tree.
     - **Back edges**: Point back to an ancestor in the DFS tree.
     - **Forward edges**: Point to a descendant that has already been visited.
     - **Cross edges**: Point between two unrelated parts of the graph.

---

#### Pseudocode

```java
EXPLORE(vertex v):
	visited[v] = TRUE
	pre[v] = clock
	clock = clock + 1
	for each edge (v, w) ∈ E:
		if NOT visited[w]:
		EXPLORE(w)
		post[v] = clock
		clock = clock + 1

DFS(Graph G):
	visited[u] = FALSE for all u ∈ V
	clock = 0
	int array pre[n], post[n]
	for v ∈ V:
		if NOT visited[v]:
		EXPLORE(v)
```

#### Applications of DFS in Directed Graphs

1. **Cycle Detection**:
   - A back edge indicates the presence of a cycle.
2. **[[Topological Sorting]]**:
   - Order vertices by decreasing post-visit times.
3. **[[Strongly Connected Components (SCCs)]]**:
   - Use DFS to identify SCCs in a directed graph.

### Pre- and Post-Visit Numbers in DFS

#### Pre- and Post-Times
1. **Pre-Visit Number**:  
   - A vertex $v$ is assigned a pre-visit number (`pre[v]`) when it is first discovered during DFS.

2. **Post-Visit Number**:  
   - A vertex $v$ is assigned a post-visit number (`post[v]`) when all its neighbors have been fully explored.

#### Example Timeline
- As DFS progresses, vertices are marked with their **pre** and **post** numbers:
  - **Pre** indicates the time when DFS visits a vertex.
  - **Post** indicates the time when DFS finishes processing a vertex.

- Example order:
  - Pre[A], Pre[B], Post[B], Pre[C], Post[C], Post[A].

#### Edge Classification Using Pre- and Post-Numbers
Given a directed edge $u \to v$ in the graph, its type can be determined based on the relative positions of `pre[u]`, `post[u]`, `pre[v]`, and `post[v]`.

1. **Tree or Forward Edge**:
   - $[ \text{pre}[u], \text{post}[u] ]$ contains $[ \text{pre}[v], \text{post}[v] ]$.
2. **Back Edge**:
   - $[ \text{pre}[v], \text{post}[v] ]$ contains $[ \text{pre}[u], \text{post}[u] ]$.
3. **Cross Edge**:
   - $[ \text{post}[v], \text{pre}[u] ]$.
4. **Impossible Case**:
   - If the intervals overlap inconsistently.

#### Key Observation
For all edges $u \to v$:
- $\text{post}[u] < \text{post}[v]$ **if and only if** $u \to v$ is a back edge.
This property is crucial for understanding the structure of DFS trees and detecting cycles in directed graphs.