---
tags:
  - algorithms
date: 2024-09-21
source: "[[COMPSCI 170]]"
---
__Median of a list:__  The $\left[ \frac{n}{2} \right]^\text{th}$ smallest number in a list of $n$ numbers.

Given an unsorted list of size $n$, finding the median of the list.

__Naive Algorithm__: 
- Sort the numbers, 
- Output the $\left[ \frac{n}{2} \right]^\text{th}$ entry. 

Runtime: Dominated by [[Quicksort|sorting]] , $O(n \log n)$

Lets solve a generalized problem.

## SELECT

SELECT is function with takes in a _unsorted_ list of size n, and integer k.
It outputs the $k^{th}$ smallest number in the list. Note,

$$Median(L) = SELECT(L, n/2)$$

### Recursive Randomized SELECT

1. Pick a pivot element $v  \in \{a_{1}, a_{2}, ..a_{n}\}$ at random.
2. Split L into 3 parts, we know the _lengths_ of these parts. This operation takes $O(n)$ time.
	1. $S_{<} = \{a_{i} | a_{i} < v\}$
	2. $S_{=} = \{a_{i} | a_{i} = v\}$
	3. $S_{>} = \{a_{i} | a_{i} > v\}$
3. Imagine as if the list was sorted,
	1. If $k \le |S_{<}|$: return $SELECT(S_{<}, k)$
	2. If $|S_{<}| \lt k \le |S_{>}| +|S_{=}|$: return $v$
	3. If $|S_{<}| + |S_{=}|\lt k$: return $SELECT(S_{>},k-|S_{<}| -|S_{=}|)$

This algorithm is _randomized_, it's runtime depends on how lucky the guess is.
So the runtime is actually the [[Expecta|expected]] runtime:

$$T[n]=\text{Expected runtime}$$

Runtime:
