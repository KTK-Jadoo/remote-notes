---
tags:
  - algorithms
date: 2024-09-03
source: "[[COMPSCI 170]]"
---
Taking the example of the [[Fibonacci Sequence]],

Let $T(n)$ be the # of _computer steps_ needed to compute `fib1(n)`.
Since, if $n <2$ the program halts immediately, $$T(n)\le2 \space for \space n \le 1$$
For large values of n, there are 2 recurrence invocations of `fib1`. Taking time $T(n-1)$ and $T(n-2)$ respectively, plus 3 steps for checking the value of $n$ and a final addition:

$$T(n) = T(n-1)+T(n-2) +3 \space for \space n > 1$$


$$$$