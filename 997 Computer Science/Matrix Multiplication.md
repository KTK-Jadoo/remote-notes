---
tags:
  - algorithms
  - compsci
  - deeplearning
date: 2024-09-05
source: "[[COMPSCI 170]]"
---
For two $n \times n$ matrices, $X$ and $Y$, we want to compute $Z=XY$

To compute the entry $Z_{i,j}$,

$$
Z_{i, j} = \sum_{k = 1}^{n} X_{i, k} Y_{k, j}
$$

This formula means that to compute the entry in the (i)-th row and (j)-th column of the matrix $Z$, you take the dot product of the (i)-th row of matrix $X$ and the (j)-th column of matrix $Y$ .

__Naive Approach__: Calculate $Z_{i,j}$ by calculating the inner product, which is $O(n)$.
Then, their are $n^{2}$ entries in the matrix, so: $O(n^3)$.


Using a [[Divide and Conquer Paradigm|Divide and Conquer]] Strategy, divide the original matrices in 4 parts, int 8 $\frac{n}{2} \times \frac{n}{2}$ matrices.

![[Screenshot 2024-09-20 at 11.43.37 PM.png]]

## Strassen's Algorithm

## Finding Triangles

