---
tags:
  - algorithms
date: 2024-12-13
source: "[[COMPSCI 170]]"
---
# Binary to Decimal Conversion (Divide-and-Conquer Solution)

## Problem Definition

- **Input**: $B[1 \dots n]$, an array of bits representing a number $B$ in binary.
- **Output**: $D[1 \dots m]$, the decimal representation of $B$ as a sequence of digits.

## Steps in the Divide-and-Conquer Algorithm

1. **Divide the Binary Array**:
   - Split the binary array $B[1 \dots n]$ into two halves:
     - Left half: $B[1 \dots \lfloor n/2 \rfloor]$.
     - Right half: $B[\lfloor n/2 \rfloor + 1 \dots n]$.
2. **Recursive Conversion**:
   - Convert the left half and the right half into their decimal values recursively.
3. **Combine Results**:
   - The decimal value of the full binary number is:$$
     \text{Decimal Value} = (\text{Left Half Decimal Value} \times 2^{\text{size of right half}}) + \text{Right Half Decimal Value}
     $$
   - The size of the right half determines the power of $2$ to multiply the left half.

## Recurrence Relation

The recurrence for this divide-and-conquer algorithm is:
$$
T(n) = 2T\left(\frac{n}{2}\right) + O(n)
$$
- $2T(n/2)$: Two recursive calls to process the left and right halves.
- $O(n)$: Combining the results (multiplying the left half by a power of $2$ and adding).

## Applying the Master Theorem
Using the Master Theorem for divide-and-conquer algorithms:
$$
T(n) = aT\left(\frac{n}{b}\right) + O(n^d)
$$
Here:
- $a = 2$ (two recursive calls),
- $b = 2$ (splitting into halves),
- $d = 1$ (the combine step is linear, $O(n)$).

We calculate:
$$
\log_b a = \log_2 2 = 1
$$
Since $d = \log_b a = 1$, the runtime is:

$$
T(n) = O(n \log n)
$$

