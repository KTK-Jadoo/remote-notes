---
title: Binary Search - Algorithms for Competitive Programming
source: https://cp-algorithms.com/num_methods/binary_search.html
published: 
author: 
created: 2024-12-10
description: The goal of this project is to translate the wonderful resource http://e-maxx.ru/algo which provides descriptions of many algorithms and data structures especially popular in field of competitive programming. Moreover we want to improve the collected knowledge by extending the articles and adding new articles to the collection.
tags:
  - clippings
  - algorithms
---

**Binary search** is a method that allows for quicker search of something by splitting the search interval into two. Its most common application is searching values in sorted arrays, however the splitting idea is crucial in many other typical tasks.

## Search in sorted arrays

The most typical problem that leads to the binary search is as follows. You're given a sorted array , check if is present within the sequence. The simplest solution would be to check every element one by one and compare it with (a so-called linear search). This approach works in , but doesn't utilize the fact that the array is sorted.

![](https://upload.wikimedia.org/wikipedia/commons/8/83/Binary_Search_Depiction.svg)  


Now assume that we know two indices such that . Because the array is sorted, we can deduce that either occurs among or doesn't occur in the array at all. If we pick an arbitrary index such that and check whether is less or greater than . We have two possible cases:

1. . In this case, we reduce the problem from to ;
2. . In this case, we reduce the problem from to .

When it is impossible to pick , that is, when , we directly compare with and . Otherwise we would want to pick in such manner that it reduces the active segment to a single element as quickly as possible *in the worst case*.

Since in the worst case we will always reduce to larger segment of and . Thus, in the worst case scenario the reduction would be from to . To minimize this value, we should pick , then

In other words, from the worst-case scenario perspective it is optimal to always pick in the middle of and split it in half. Thus, the active segment halves on each step until it becomes of size . So, if the process needs steps, in the end it reduces the difference between and from to , giving us the equation .

Taking on both sides, we get .

Logarithmic number of steps is drastically better than that of linear search. For example, for you'd need to make approximately a million operations for linear search, but only around operations with the binary search.

### Lower bound and upper bound¶

It is often convenient to find the position of the first element that is greater or equal than (called the lower bound of in the array) or the position of the first element that is greater than (called the upper bound of) rather than the exact position of the element.

Together, lower and upper bounds produce a possibly empty half-interval of the array elements that are equal to . To check whether is present in the array it's enough to find its lower bound and check if the corresponding element equates to .

### Implementation

The explanation above provides a rough description of the algorithm. For the implementation details, we'd need to be more precise.

We will maintain a pair such that . Meaning that the active search interval is . We use half-interval here instead of a segment as it turns out to require less corner case work.

When , we can deduce from definitions above that is the upper bound of . It is convenient to initialize with past-the-end index, that is and with before-the-beginning index, that is . It is fine as long as we never evaluate and in our algorithm directly, formally treating it as and .

Finally, to be specific about the value of we pick, we will stick with .

Then the implementation could look like this:

```java
... // a sorted array is stored as a[0], a[1], ..., a[n-1]
int l = -1, r = n;
while (r - l > 1) {
    int m = (l + r) / 2;
    if (k < a[m]) {
        r = m; // a[l] <= k < a[m] <= a[r]
    } else {
        l = m; // a[l] <= a[m] <= k < a[r]
    }
}
```

During the execution of the algorithm, we never evaluate neither nor , as . In the end, will be the index of the last element that is not greater than (or if there is no such element) and will be the index of the first element larger than (or if there is no such element).

**Note.** Calculating `m` as `m = (r + l) / 2` can lead to overflow if `l` and `r` are two positive integers, and this error lived about 9 years in JDK as described in the [blogpost](https://ai.googleblog.com/2006/06/extra-extra-read-all-about-it-nearly.html). Some alternative approaches include e.g. writing `m = l + (r - l) / 2` which always works for positive integer `l` and `r`, but might still overflow if `l` is a negative number. If you use C++20, it offers an alternative solution in the form of `m = std::midpoint(l, r)` which always works correctly.

## Search on arbitrary predicate

Let be a boolean function defined on such that it is monotonously increasing, that is

The binary search, the way it is described above, finds the partition of the array by the predicate , holding the boolean value of expression. It is possible to use arbitrary monotonous predicate instead of . It is particularly useful when the computation of is requires too much time to actually compute it for every possible value. In other words, binary search finds the unique index such that and if such a *transition point* exists, or gives us if or if .

Proof of correctness supposing a transition point exists, that is and : The implementation maintaints the *loop invariant* . When , the choice of means will always decrease. The loop terminates when , giving us our desired transition point.

```
... // f(i) is a boolean function such that f(0) <= ... <= f(n-1)
int l = -1, r = n;
while (r - l > 1) {
    int m = (l + r) / 2;
    if (f(m)) {
        r = m; // 0 = f(l) < f(m) = 1
    } else {
        l = m; // 0 = f(m) < f(r) = 1
    }
}
```

### Binary search on the answer

Such situation often occurs when we're asked to compute some value, but we're only capable of checking whether this value is at least . For example, you're given an array and you're asked to find the maximum floored average sum

among all possible pairs of such that . One of simple ways to solve this problem is to check whether the answer is at least , that is if there is a pair such that the following is true:

Equivalently, it rewrites as

so now we need to check whether there is a subarray of a new array of length at least with non-negative sum, which is doable with some prefix sums.

## Continuous search

Let be a real-valued function that is continuous on a segment .

Without loss of generality assume that . From [intermediate value theorem](https://en.wikipedia.org/wiki/Intermediate_value_theorem) it follows that for any there is such that . Note that, unlike previous paragraphs, the function is *not* required to be monotonous.

The value could be approximated up to in time for any specific value of . The idea is essentially the same, if we take then we would be able to reduce the search interval to either or depending on whether is larger than . One common example here would be finding roots of odd-degree polynomials.

For example, let . Then and with and . Which means that it is always possible to find sufficiently small and sufficiently large such that and . Then, it is possible to find with binary search arbitrarily small interval containing such that .

## Search with powers of 2

Another noteworthy way to do binary search is, instead of maintaining an active segment, to maintain the current pointer and the current power . The pointer starts at and then on each iteration one tests the predicate at point . If the predicate is still , the pointer is advanced from to , otherwise it stays the same, then the power is decreased by .

This paradigm is widely used in tasks around trees, such as finding lowest common ancestor of two vertices or finding an ancestor of a specific vertex that has a certain height. It could also be adapted to e.g. find the \-th non-zero element in a Fenwick tree.

## Practice Problems

- [LeetCode - Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
- [LeetCode - Search Insert Position](https://leetcode.com/problems/search-insert-position/)
- [LeetCode - First Bad Version](https://leetcode.com/problems/first-bad-version/)
- [LeetCode - Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/)
- [LeetCode - Find Peak Element](https://leetcode.com/problems/find-peak-element/)
- [LeetCode - Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- [LeetCode - Find Right Interval](https://leetcode.com/problems/find-right-interval/)
- [Codeforces - Interesting Drink](https://codeforces.com/problemset/problem/706/B/)
- [Codeforces - Magic Powder - 1](https://codeforces.com/problemset/problem/670/D1)
- [Codeforces - Another Problem on Strings](https://codeforces.com/problemset/problem/165/C)
- [Codeforces - Frodo and pillows](https://codeforces.com/problemset/problem/760/B)
- [Codeforces - GukiZ hates Boxes](https://codeforces.com/problemset/problem/551/C)
- [Codeforces - Enduring Exodus](https://codeforces.com/problemset/problem/645/C)
- [Codeforces - Chip 'n Dale Rescue Rangers](https://codeforces.com/problemset/problem/590/B)

