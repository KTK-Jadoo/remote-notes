---
tags:
  - algorithms
date: 2024-10-30
source: "[[COMPSCI 170]]"
---
One of the two _sledgehammers_ of the algorithms craft. Very broadly applicable, with a predictable cost in efficiency. 

__Dynamic Programming__ is a very powerful algorithmic paradigm in which a problem is solved by identifying a collection of subproblems and tackling then one by one, smallest first, using the answers to small problems  to help figure out the larger ones, until the whole lot of them are solved.

## Visualizing Dynamic Programs

The special distinguishing feature of a dag is that it's nodes can be _linearized_, i.e. they can be arranged in a line such that all all edges go from left to right (topological ordering).

![[Pasted image 20241030184326.png]]

If we want to figure out the distance from node S to all the other nodes. 
For example if the other node is D, we can only get to D from B or C. So we can simply choose the smaller of the two. $$dist(S, D) = min\{dist(S, B)+1,dist(S, C)+3\}$$
A similar relation follows for every other node. So it feels very recursive. 

```pcode
initialize all dist(·) values to ∞
dist(s) = 0
for each v ∈ V \{s}, in linearized order:
dist(v) = min(u,v)∈E {dist(u) + l(u, v)}
```

So this algorithm is solving a collection of _subproblems_ $\{dist(u): u \in V\}$.
We start with the smallest one, $dist(s)$ since we know it to be 0, and we proceed with progressively "larger" subproblems: distances to vertices that that further and further along the linearized DAG. 

So in this general technique, at each node we compute some function of the values of the node's predecessor. If we chose a $\max$ instead of a $\min$ we would compute the _longest paths_
in the DAG. Or if we multiply instead of adding inside the brackets, we get the path with smallest product of edge lengths.

We may not be given a dag, but the dag is _implicit_, i.e. it's nodes are the subproblems we define and it's edges are the dependencies between the subproblems: if in order to solve problem B we need the answer to problem A, there is a (conceptual) edge between (A, B). In this case, A is considered "smaller" than B.


Approach:

1) Define appropriate _subproblems_. 
	1) The largest one essentially solves the problem
2) Write a _recurrence relation_.
	1) With a base case
3) Determine _order_ of computation
	1)  Induces a DAG structure


### Longest Increasing Subsequence

Given input is the sequence of numbers: $a_{1}, a_{2}, a_{3}, \dots a_{n}$
A subsequence is any subset of numbers, taken _in order_, 
of the form $a_{i_{1}}, a_{i_{2}}, \dots a_{i_{k}}$, where, $1<i_{1}<i_{2}\dots <i_{k}\le n$.

An _increasing_ subsequence is one where the number are _strictly_ getting larger. 

The task is to find the increasing subsequence of the greatest length.

![[Pasted image 20241030192220.png]]


To create this DAG, we create a graph of all permissible (transitions) edges. 
Establish a node $i$, for each element $a_{i}$ and add directed edges $(i, j)$ s.t. $i < j$, and $a_i < a_j$.

So now we just have to find the longest path in this DAG!

```pcode
for j = 1, 2, . . . , n:
L(j) = 1 + max{L(i) : (i, j) ∈ E}
return maxj L(j)
```

The L-values only tell us the _length_ of the longest subsequence. To recover the subsequence, while computing $L(j)$ we note down $prev(j)$, the next to last node on the longest path to $j$. The optimal subsequence can be reconstructed following these backpointers.


 >[!note] Why Recursion doesn't work here
 >In divide and conquer, a problem is expressed in term sof subproblems that are substantially smaller, because of which the full recursion tree is only logarithmic depth and a polunomial number of nodes.
 ><br>
 >In typical dynamic programming, a problem is reduced to only slightly smaller subproblems. Like how $L(j)$ relies on $L(j-1)$. Thus the full recursion tree has polynomial depth and exponential number of nodes. However, most of these nodes are repeats, Efficiency is therefore obtained by enumerating the distinct subproblems and solving them in the right order.
 >


### Edit Distance

Edit distance is the minimum number of edits—insertions, deletions, and substitutions of characters needed to transform the first string into the second. For instance, the alignment shown on the left corresponds to three edits: insert U, substitute O → N, and delete W.

 There is an ordering on the subproblems, and a relation that shows how to solve a subproblem given the answers to “smaller” subproblems, that is, subproblems that appear earlier in the ordering.


##### Common subproblems

Finding the right subproblem takes creativity and experimentation. But there are a few standard choices that seem to arise repeatedly in dynamic programming.

![[Pasted image 20241030212521.png]]

![[Pasted image 20241030212536.png]]

![[Pasted image 20241030212546.png]]

![[Pasted image 20241030212555.png]]

