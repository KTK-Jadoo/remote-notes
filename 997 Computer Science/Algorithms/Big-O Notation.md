---
tags:
  - "#algorithms"
  - math
date: 2024-05-29
source: "[[COMPSCI 170]]"
---
# Definition

A way to approximately measure the runtime of an algorithm. 

Let $T[n]$ be the time taken by an algorithm on an input $n$.
- Depends on computer, processor, language etc


### $O$ Notation

>[!note] Formal Definition of Big-O Notation
>Let $f:\mathbb{N}\rightarrow\mathbb{N}$ and $g:\mathbb{N}\rightarrow\mathbb{N}$
>We say that $f = O(g) \iff$ f grows no faster than g $\iff$ f is almost $C \cdot g$ so, $\exists$ constant $C$ s.t $$f(n) \le C \cdot g(n)$$

Observations on common functions:
- $poly(n) = O(n^{degree})$
- $n^{3}=O(n^{4}) \iff \space n^{3} \text{ grows no faster than } n^{4}$
- Any polynomial in n $= O(2^{n})$
- $\log(n) = O(\text{any polynomial in n})$


### $\Theta$ Notation

>[!note] Formal Definition of $\Theta$ Notation
>We say $f=\Theta(g)$ ,
>if $f=O(g)$ AND $g=O(f) \iff f\approx g$


### $\Omega$ Notation

>[!note] Formal Definition of $\Omega$ Notation
>We say $f=\Omega(g) \iff f = O(g)$ 



### Asymptotic Limit Rules

- If $\lim_{ n \to \infty } \frac{f(n)}{g(n)} = 0,$ then $f(n) = O(g(n))$
- If $\lim_{ n \to \infty } \frac{f(n)}{g(n)} = c,$ where $c \gt 0,$ then $f(n) = \Theta(g(n))$
- If $\lim_{ n \to \infty } \frac{f(n)}{g(n)} = \infty,$ then $f(n) = \Omega(g(n))$


