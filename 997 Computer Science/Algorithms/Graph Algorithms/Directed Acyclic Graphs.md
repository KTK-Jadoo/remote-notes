---
tags:
  - algorithms
date: 2024-12-15
source: "[[COMPSCI 170]]"
---
# Directed Acyclic Graphs (DAGs)

#### Definition
- A **Directed Acyclic Graph (DAG)** is a directed graph with **no directed cycles**.
#### Applications
1. **Modeling Dependencies / Pre-Requisites**:
   - Example: Course prerequisites.
     - A course can only be taken if all its prerequisites are completed, forming a DAG of dependencies.
   - Example: Source files for compilation.
     - Files must be compiled in a specific order, respecting dependencies between them.

### Topological Sort [Linearization of a DAG]
#### Problem Statement
- **Input**: A directed acyclic graph $G = (V, E)$.
- **Output**: An ordering of vertices such that for every directed edge $u \to v$, $u$ appears **before** $v$ in the ordering.
  - This "linearizes" the DAG.

---

#### Algorithm

1. **Run [[Depth First Search|DFS]]** to compute pre- and post-visit numbers for all vertices.
2. **Sort vertices in decreasing order of post-visit numbers** to produce the topological order.

---

#### Proof of Correctness

1. **Key Observation**:  
   - By earlier properties of DFS, for an edge $u \to v$, $\text{post}[u] > \text{post}[v]$ if and only if $u \to v$ is a back edge.
   - A DAG has **no back edges**, ensuring that the above condition holds for all edges in decreasing order of post-visit numbers.

2. **No Back Edges in DAG**:  
   - Since DAGs are acyclic, all edges follow the condition $\text{post}[u] > \text{post}[v]$.

3. **Output**:  
   - Sorting vertices by decreasing post-visit numbers ensures all edges point **from left to right** in the topological ordering.

#### Example of Topological Sort
1. Perform DFS to compute pre- and post-visit numbers.
2. Order vertices in decreasing post-visit numbers.
3. Linearize the graph as the final result.