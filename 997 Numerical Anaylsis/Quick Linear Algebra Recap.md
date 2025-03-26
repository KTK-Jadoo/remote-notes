---
tags:
  - "#math"
date: 2025-02-03
source: "[[MATH 156]]"
---
## Vectorspaces

A vectorspace $V$ over a field $K$ (usually either $\mathbb{R} \text{ or } \mathbb{C}$) is a set of vectors we can add together or multiply by a scalar.

The particular axioms are in Math 113 (Abstract Algebra).

Example: 
1) $\mathbb{R}^n$ or $\mathbb{C}^n$, $\vec{x} = \begin{bmatrix} x_{1} \cr x_{2} \cr .. \cr x_{n}\end{bmatrix}$, where $\forall x_{i} \in \mathbb{R} \text{ or }  \mathbb{C}$.
2) Polynomials of degree $\le n$ , combining polynomials creates a linear combination (linear vector space)
3) $C[a, b]$ = continuous function on $[a, b]$
$$(\alpha f + \beta g) (x) = \alpha f(x)+\beta g(x)$$

### Span and Linear Dependence

If $x_{1}, x_{2}, \dots x_{n} \in V$, the Span(V) is the set of all linear combinations $$\alpha_{1}\vec{x_{1}} + \alpha_{2}\vec{x_{2}} \dots \dots+ \alpha_{n}\vec{x_{n}}$$
for $\alpha_{i} \in K$, 
Span of the empty set is $\vec{0}$.

A finite set of vectors {$x_{i}$} is _linearly dependent_ if $\exists$ a corresponding set {$\alpha_{i}$} of scalars, _not all zero_ (non-trivial), such that: $$\sum_{i} \alpha_{i}x_{i} = 0$$
If the above implies that all entries of $\alpha$ need to be = 0, set{$x_i$} is _linearly independent_.

___Theorem 1:___ $\vec{x_{1}},\vec{x_{2}},\vec{x_{3}}, \dots \vec{x_{n}}$ are linearly dependent $\iff$ one of the $\vec{x_{k}}$ with $k \ge 2$ if a linear combination of it's predecessors.

__Cor 1.1:__ If a set of linearly dependent vectors don't span V, $\exists$ $x_{k+1} \in V$, , which can be added to the set while staying linearly independent.

__Cor 1.2:__ If $\vec{x_{1}},\vec{x_{2}},\vec{x_{3}}, \dots \vec{x_{m}}$ span V, and $\exists k \le 2$  and $\beta_{i}$ such that:
$$\vec{x_{k}} = \beta x_{1} + \beta_{2}x_{2} \dots \beta_{k-1}x_{k-1}$$
then we can drop $\vec{x_{k+1}},\dots \vec{x_{m}}$ if $k = m$, and still span V.

___Theorem 2:___ If $\vec{x_{1}},\vec{x_{2}},\vec{x_{3}}, \dots \vec{x_{m}}$ span V, and $\vec{y_{1}},\vec{y_{2}},\vec{y_{3}}, \dots \vec{y_{n}}$, are linearly independent, then $m \ge n$


### Basis

A (linear) basis (or a coordinate system) in a vector space  $V$ is a set $X$ of linearly independent vectors such that every vector in $V$ is a linear combination of elements of $X$.  A vector space $V$ is __finite - dimensional__ if it has a finite basis.

The dimension of a finite-dimensional vector space $V$ is the number of elements in a basis of $V$.

__Cor 2.1:__ Any linearly independent spanning set is well defined, for any bases for V.

__Cor 2.2:__ If dim(V) = n, and $\vec{y_{1}},\vec{y_{2}},\vec{y_{3}}, \dots \vec{y_{n}}$ are lin ind, $\vec{y_{1}},\vec{y_{2}},\vec{y_{3}}, \dots \vec{y_{n}}$ is a basis for $V$.

In infinite dimensions, you need a topology so you can take limits. This changes a lot of the theory and analysis techniques.

__Cor 1.3:__ Subspace extending to create Basis.

___Theorem 3:___ If $\vec{y_{1}},\vec{y_{2}},\vec{y_{3}}, \dots \vec{y_{n}}$ is a basis for $V$, every element $\vec{x} \in V$ has a unique decomposition as a linear combination of the basis.

Remember Standard Basis vectors from Math 56.


### Isomorphism

A one-to-one correspondence between two linear spaces over the same field that maps sums into sums and scalar multiples into scalar multiples is called an __isomorphism__.  

Isomorphism is a basic notion in linear algebra. Isomorphic linear spaces are indistinguishable by means of operations available in linear spaces. Two linear spaces that are presented in very different ways can be, as we have seen, isomorphic.

Two vector spaces $V$ and $U$ (over the same field) are __isomorphic__ if there is a one-to-one correspondence between the vectors x of $V$ and the vectors y of $U$, say $y = T(x)$, such that:  $$T(\alpha_{1}x_{1} + \alpha_{2}x_{2}) = \alpha_{1}T(x_{1}) + \alpha_{2}T(x_{2})$$
In other words, $V$ and $U$ are isomorphic if there is an isomorphism (such as T) between them, where an isomorphism is a one-to-one correspondence that preserves all linear relations


### Subspaces

A non-empty subset $\mathbb{M}$ of a vector space $V$ is a _subspace_ or a _linear manifold_ if along with every pair, $x$ and $y$, of vectors contained in $\mathbb{M}$, every linear combination $\alpha x + \beta y$ is also contained in $\mathbb{M}$.

A subspace is a vectorspace in it's own right, and had dim $\le$ dim{V}.


## Linear Operators (Matrices)

If V, W are two vector spaces, over K, then a function $A: V \rightarrow W$ is a _linear operator_, if

$$A(x+y) = Ax +Ay$$$$A(\alpha x) = \alpha Ax$$
holds. ___Linear operators from V to W form a vector space___.
$$(\alpha A + \beta B)x = \alpha(Ax) + \beta(Bx)$$
The space of an $m \times n$ matrix can be imagined as linear operators from $\mathbb{R}^{n}\rightarrow \mathbb{R}^m$.
The columns of A are vectors in $\mathbb{R}^m$, one can view matrix-vector multiplication as a rule to extract linear combinations of the columns.

Matrix - Matrix Products $\rightarrow$ Composition of Linear Operators

## Invertibility

A $n \times n$ matrix $A$ is invertible if $\exists B$ s.t, $AB = I$.
Implies A is injective (1-1), the only vector with A$\vec{x}$ = 0 is $\vec{x}$ = 0
So was can manually contruct the inverse.