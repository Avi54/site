---
title:  "A Solution to the Dutch National Flag problem"
date:   2025-06-22
draft: false
tags:   
- programming
---
Presenting a solution to the [Dutch National Flag](https://en.wikipedia.org/wiki/Dutch_national_flag_problem) problem.

## Algorithim

```python
def dutch(A, n): 
    i = 0
    j = 0
    k = n - 1

    while (j <= k):
        if (A[i] == 1):
            A[i], A[j] = A[j], A[i]
            i = i + 1
            j = j + 1
        elif (A[j] == 3):
            A[j], A[k] = A[k], A[j]
            k = k - 1
        else:
            j = j + 1
```

## Time and Space Complexity
$T(n) = \begin{cases}
        0 & \text{ if } n = 0 \text{ or } n = 1 \newline
        T(n - 1) + 1 & \text{ ow }
\end{cases}$

$T(n) \sim O(n)$ and $S(n) \sim O(1)$