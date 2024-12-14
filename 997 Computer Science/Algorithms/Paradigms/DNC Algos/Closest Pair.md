---
tags:
  - algorithms
date: 2024-12-13
source: "[[COMPSCI 170]]"
---
# Closest Pair

#### High-Level Approach
The closest pair of points problem involves finding the two points in a set of $n$ points (in 2D space) that are the closest to each other based on Euclidean distance. The [[Divide and Conquer]] algorithm splits the problem into smaller subproblems and combines their results efficiently.

#### Steps in the Divide-and-Conquer Algorithm
1. Sort the Points by X-Coordinate:
   - The points are initially sorted by their $x$-coordinates, which takes **$O(n \log n)$**.
2. Divide the Points:
   - Split the points into two halves at the midpoint. This step takes **$O(1)$**.
3. Solve the Subproblems Recursively:
   - Recursively find the closest pair in the left half and the right half.
   - For a set of $n$ points, this leads to two recursive calls of size $n/2$ each, contributing to **$2T(n/2)$** in the recurrence.
4. Merge Step (Combine Results):
   - Identify the closest pair spanning across the dividing line:
     - Consider only the points within a strip of width $2\delta$ (where $\delta$ is the minimum distance from the left and right halves).
     - Sort the strip points by their $y$-coordinates if needed.
     - For each point in the strip, compare it with the next 7 points (constant comparisons).
   - The merge step works in **$O(n)$** time.

#### Recurrence Relation
The recurrence relation for the runtime is:
$$
T(n) = 2T\left(\frac{n}{2}\right) + O(n)
$$
- $2T(n/2)$: Recursive calls to solve the left and right halves.
- $O(n)$: Work done in the merge step (linear processing of the strip).

#### Applying the Master Theorem
The recurrence can be analyzed using the [[Master Theorem]] for divide-and-conquer algorithms:
$$
T(n) = aT\left(\frac{n}{b}\right) + O(n^d)
$$
Here:
- $a = 2$ (two recursive calls),
- $b = 2$ (splitting into halves),
- $d = 1$ (the merge step is $O(n)$, linear work).
We calculate:
$$
\log_b a = \log_2 2 = 1
$$
Since $d = \log_b a = 1$, the runtime is dominated by **$O(n \log n)$** according to the Master Theorem.

#### Breaking Down the Runtime

1. **Sorting by $x$-coordinate (initial step)**:
   - Sorting takes **$O(n \log n)$**.
2. **Recursive Calls**:
   - Solving the left and right halves contributes to **$O(n \log n)$** (derived from the recurrence).
3. **Merge Step**:
   - Combining results requires **$O(n)$** per level of recursion.
   - Across $\log n$ levels, this totals to **$O(n \log n)$**.
