---
tags:
  - algorithms
date: 2024-09-20
source: "[[COMPSCI 170]]"
---
# Definition

Suppose function $T: \mathbb{N} \to \mathbb{R}^{+}$ (input to time), and satisfies, $$T[n] = a \cdot T \left[ \frac{n}{b} \right] +O(n^{c})$$
where, $b>1$, $a,c>0$ are constants.

- Case 1: If $c< \log_{b}a \implies T[n] = O(n^{\log_{b}a})$
- Case 2: If $c= \log_{b}a \implies T[n] = O(n^{c}\log n)$
- Case 3: If $c > \log_{b}a \implies T[n] = O(n^{c})$

Looking at $T$:
- depth = $\log_{b}n$
-  # Nodes in tree = $1+a^{2}+a^{3}\dots a^\text{depth}$, which is a Geometric Progression
	- = $O(a^\text{depth})$ = $O(a^{\log_{b}n})$ = $O(n^{\log_{b}a})$

