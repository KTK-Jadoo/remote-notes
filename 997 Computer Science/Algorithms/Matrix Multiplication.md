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

**Matrix-Multiply** (X, Y : n × n matrices)

- Think of $X, Y$ as a $2 \times 2$ array of $\frac{n}{2} \times \frac{n}{2}$ matrices:

$$
X = \begin{bmatrix} A & B \\ C & D \end{bmatrix}, \quad
Y = \begin{bmatrix} E & F \\ G & H \end{bmatrix}
$$

- Matrix product $XY$:

$$
XY = \begin{bmatrix} AE + BG & AF + BH \\ CE + DG & CF + DH \end{bmatrix}
$$

- Compute matrix products (using recursion):

$$
P_1 = A(F - H), \quad P_2 = (A + B)H, \quad P_3 = (C + D)E
$$
$$
P_4 = D(G - E), \quad P_5 = (A + D)(E + H), \quad P_6 = (B - D)(G + H), \quad P_7 = (A - C)(E + F)
$$

- Output:

$$
\begin{bmatrix}
P_5 + P_4 - P_2 + P_6 & P_1 + P_2 \\
P_3 + P_4 & P_1 + P_5 - P_3 - P_7
\end{bmatrix}
$$

Modern quickest way to matrix multiply: https://deepmind.google/discover/blog/discovering-novel-algorithms-with-alphatensor/


## Application: Finding Triangles

