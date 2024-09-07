---
tags:
  - "#algorithms"
  - math
date: 2024-05-29
source: "[[COMPSCI 170]]"
---
Taking the [[Fibonacci Sequence]] as an example, when designing an algorithm we need to see:


Let $T[n]$ = time taken on input of size n  

Approximate since different hardware can have different results

Function $f:N\to N$ and $g: N \to N$
so,
$f = O(g)$
F grows no faster than g
f is almost C . g

$\exists C :  f(n) \le C. g(n), \forall n$

#### Observations
- Poly (n) = O($n^{degree}$)
- $n^3$ = $O(n^4)$ (n cube grows no faster than n^4)


F = theta(g)
if f = O(g)  AND g = O(f)
f ~ g


Back to fibonnaci

Making tree diagram

n depth
T(n) = # of function calls



### Problem solving tips

__Discussion 1__:
 
 (a) $$
 L'hopital's \space Rule \rightarrow \frac{6}{24}
 \rightarrow \space < \infty, \therefore n^{3}=O(n^4)

$$
(b) 
$$
f(n) = n
, \space
g(n) = 2n
$$
$$f(n)=\Theta(g(n))\implies f(n) = O(g(n))$$


(c)

Q2

(b)
(i)$$
Limit = \frac{3}{4}\therefore f(n)=\Theta(g(n))$$
Differ by constant multiple.

(ii)$$\lim_{n \rightarrow \infty}\frac{nlog(n^4)}{n^{2}log(n^{3)}}$$
$$\lim_{n \rightarrow \infty}\frac{4nlog(n)}{3n^{2}log(n}$$



So limit is 0

(iii) $$
L'Hopital's Rule \space,
f(n) = \Omega(g(n))
$$
(iv)
$$f(n) = \Theta (g(n))$$

Q3 

Runtime of recursive functions:

- Standard $T(n) = aT\left(\frac{n}{b}\right)+ \theta[n^d]$
- a = # of subproblems
- b = relative input size
- Last term = processing time


### Master's Theorem


\# Layer's: $log_{b}(n)$
\# Leaves : $a^{\#layers}$= solves to $n^{log_{b}(a)}$

- Top recursive layer dominates 
- $O(n^{d})log(n)$
- bottom layer dominates

![[dis01.pdf#page=3&rect=60,261,512,463]]

(a)
\#layers = $log_{2}(n)$
\#leaves = $2^{\# layers}$ = $2^{log_{2}(n)}$=$n^{log_{2}(2)}$=n

d = 1`

Therefore Using Master's Theorem:

$T(n) = O (n log(n))$




(b)

Series expansion
T[n] = 1+2+3 ... n

n(n+1)/2
T(n) O(n^2)
\#layer = $log(n-1)$
\#leaves = 
