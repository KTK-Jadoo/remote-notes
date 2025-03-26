---
tags:
  - "#math"
date: 2025-02-03
source: "[[MATH 156]]"
---
## Vectorspaces

A vectorspace $V$ over a field $K$ (usually either $\mathbb{R} \text{ or } \mathbb{C}$) is a set of vectors that satisfy the following axioms:

1) To every pair, $x$ and $y$, of vectors in $V$ there corresponds a vector $x + y$, called the sum of $x$ and $y$, in such a way that  
	- addition is commutative, $x + y = y + x$,  
	- addition is associative, $x + (y + z) = (x + y) + z$,  
	- there exists in $V$ a unique vector $\vec{0}$ (called the origin) such that $x + 0 = x$ for every vector $x$, and to every vector $x$ in $V$ there corresponds a unique vector $-x$ such that $x + (-x) = 0$.

2) To every pair, $a$ and $x$, where $a$ is a scalar and $x$ is a vector in $V$, there corresponds a vector $ax$ in $V$, called the product of $a$ and $x$, in such a way that :
- multiplication by scalars is associative, $a(bx) = (ab)x$, 
- $1x = x$ for every vector $x$.
- multiplication by scalars is distributive with respect to vector addition, $a(x + y) = ax + ay$.
- multiplication by vectors is distributive with respect to scalar addition, $(a + b)x = ax + bx$.

We mention in passing that if the scalars are elements of a ring (instead
of a field), the generalized concept corresponding to a vector space is  
called a module.

### Linear Dependence

A finite set of vectors {$x_{i}$} is _linearly dependent_ if $\exists$ a corresponding set {$\alpha_{i}$} of scalars, _not all zero_, such that: $$\sum_{i} \alpha_{i}x_{i} = 0$$
If the above implies that all entries of $\alpha$ need to be = 0, set{$x_i$} is _linearly independent_.

### Basis

A (linear) basis (or a coordinate system) in a vector space  $V$ is a set $X$ of linearly independent vectors such that every vector in $V$ is a linear combination of elements of $X$.  A vector space $V$ is __finite - dimensional__ if it has a finite basis.

The dimension of a finite-dimensional vector space $V$ is the number of elements in a basis of $V$.

### Isomorphism

A one-to-one correspondence between two linear spaces over the same field that maps sums into sums and scalar multiples into scalar multiples is called an __isomorphism__.  

Isomorphism is a basic notion in linear algebra. Isomorphic linear spaces are  
indistinguishable by means of operations available in linear spaces. Two linear  
spaces that are presented in very different ways can be, as we have seen, isomorphic.

Two vector spaces $V$ and $U$ (over the same field) are __isomorphic__ if there is a one-to-one correspondence between the vectors x of $V$ and the vectors y of $U$, say 
$y = T(x)$, such that:  $$T(\alpha_{1}x_{1} + \alpha_{2}x_{2}) = \alpha_{1}T(x_{1}) + \alpha_{2}T(x_{2})$$
In other words, $V$ and $U$ are isomorphic if there is an isomorphism (such  
as T) between them, where an isomorphism is a one-to-one correspondence  
that preserves all linear relations



## Subspaces

The objects of interest in geometry are not only the points of the space under consideration, but also its lines, planes, etc. We proceed to study the analogues, in general vector spaces, of these higher-dimensional elements.  

A non-empty subset $\mathbb{M}$ of a vector space $V$ is a _subspace_ or a _linear manifold_ if along with every pair, $x$ and $y$, of vectors contained in $\mathbb{M}$, every linear combination $\alpha x + \beta y$ is also contained in $\mathbb{M}$.



