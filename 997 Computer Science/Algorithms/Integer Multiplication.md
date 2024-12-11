---
tags:
  - algorithms
  - math
date: 2024-09-17
source: "[[COMPSCI 170]]"
---
Most architectures don't support $>64$ bit integers. Eg Cryptography

## Integer Addition

Suppose we take a fixed __Integer__ ($64$bit):
- To store $f(n)$, each addition is one machine instruction ($O(1)$), so
$$T(n) = O(n)$$
But, how many bits long will the $n^{th}$ Fibonacci number be?

- ! Any number $X$ is __$\log _{2} X$__ bits long. 

So, we need [[Python Data Structures|Big Integer]] data type (stored as a sequence of digits in an [[Python Data Structures|array]]).


## Integer Multiplication

Input: 2 n-digit Big Integers, $a, b$ 
Goal: $c = a \times b$, where $c$ is a 2n-digit number

Runtime: $O(n^{2})$
- $n$ numbers, each of which is $n$ digits long (adding n, n digit numbers)

[[Analysis of Algorithms|Can we do better?]]

Using a [[Divide and Conquer Paradigm|Divide and Conquer Algorithm]],

Split input arrays into $a = a_{L} + a_{R}$ and $b = b_{L} + b_{R}$.

Eg: $$123456 \rightarrow (123)10^{3}+456$$
So, $$a = 10^{\frac{n}{2}}a_{L}+a_{R}$$$$b = 10^{\frac{n}{2}}b_{L}+b_{R}$$
And, $$a \times b = 10^{\frac{n}{2}}a_{L}b_{L} + 10^{\frac{n}{2}}[a_{L}b_{R}+a_{R}b_{L}] + a_{R}b_{R}$$
which are $4$ products of $\frac{n}{2}$ digit numbers.

Implementation in [[Python Data Structures|py]] using some [[Bit Manipulation|bit manipulation]].

Runtime: $T[n]  =$ Time taken by `multiply` on n-digit numbers,
$$T[n] = 4 \cdot T\left[ \frac{n}{2} \right ]+ C \cdot n \text{ (additions with Order n)}$$
where $C$ is some constant.

![[Screenshot 2024-09-20 at 9.58.30 PM.png]]

Total work done: $$1 \cdot C \cdot n + 4\left( C \cdot \frac{n}{2} \right) + \dots 4^{k}\left( C \cdot \frac{n}{2^{k}} \right) + 4^{\log n} \left( C \cdot \frac{n}{2^{\log n}} \right)$$
- ! Sum of $n$ term Geometric Progression $\approx O \text{ (last term / largest term)}$. Largest term if ratio $r \gt 1$.


So, applying to the problem at hand,$$= O\left( C \cdot n \cdot \frac{4^{\log n}}{2^{\log n}} \right)$$
- ! $2^{\log n} = n$
$$ = O(C \cdot n \cdot n) = O(n^{2})$$
Still same as grade school Multiplication, however, we can it faster. Change n-digit multiplication, to 3 n/2 digit multiplications. 

__Karatsuba's Algorithm__ would run in:

$$= O\left( C \cdot n \cdot \frac{3^{\log n}}{2^{\log n}} \right)$$
- ! $a^{\log b} = b^{\log a}$

- ! $2^{\log n} = n$
$$= O(n^{\log 3}) \approx O(n^{1.7})$$
#### Karatsuba's Algorithm

$$a \cdot b = 10^{\frac{n}{2}}a_{L}b_{L} + 10^{\frac{n}{2}}[a_{L}b_{R}+a_{R}b_{L}] + a_{R}b_{R}$$
$$= 10^{\frac{n}{2}}a_{L}b_{L} + 10^{\frac{n}{2}}[(a_{L}+a_{R})(b_{L}+b_{R})-a_{L}b_{L} -a_{R}b_{R}] + a_{R}b_{R}$$

Which is only has 3 products of $\frac{n}{2}$ digits.

Now, the fastest time for Integer Multiplication is $O(n \cdot \log n)$.




