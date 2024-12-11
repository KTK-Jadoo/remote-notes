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

![[Screenshot 2024-10-01 at 4.56.53 PM.png]]


## Exponentiation (Using Karatsuba's Algorithm)

Inputting a number, we want the the exponentiated number from it.

```pcode
EXP(a, n:integer)
	if n=1 return a
	B = EXP(a, [n/2])
	if n is even return B*B
	if n is odd return B*B*a
```

Runtime: $a^{n},a^{\frac{n}{2},}, a^{\frac{n}{4},} \dots a^{1}$
$$T[n]= T\left[ \frac{n}{2} \right] + \Theta(M(n))$$

Where M(n) is time to multiple 2 n digit numbers, say [[Integer Multiplication#Karatsuba's Algorithm]]

By Master Theorem: $$T[n] = M(n)$$

## Binary to Decimal

Covert an array of bits to decimal representation of number as a sequence of digits.

Naive: $\Theta(n) \text{ additions} \rightarrow \Omega(n^2)$

Divide and Conquer Approach: 

- Split array into 2 halves.
	- $a_{L}, a_{R}$ 
- Recurse:
	- $d_{L}$ -> BinarytoDecimal($a_{L}$)
	- $d_{R}$ -> BinarytoDecimal($a_{R}$)
	- c => $EXP(2,n/2)$
- Combine:
	- Return $d_{L}*c + d_{R}$

Runtime:
$$T[n] = 2T\left[ \frac{n}{2} \right] + \text{Time to multiply}+\text{ Time to add}$$
$$T[n]=M(n)$$

## Closest Pair

$n$ points on a plane, find the closest pair. 

Naively, $\Theta(n^2)$

DNC approach:

Split the plane:

- Sort the points, $p_{1}, .. p_{n}$ in increasing x coordinate.
- Split sorted list in order to have split the list in 2 equal parts.

Recurse:
- Find closed on $S_left$
- and closest on $S_right$

Use than closest distance to only look at crossing lines that are at most d way from the line.

But if most or all points lie in the area, we can only look at the subregion which is opposite to the direction a point lies and look $d$ up and down. So a $d \times 2d$ region.

$T[n] = O(n\log n)$
