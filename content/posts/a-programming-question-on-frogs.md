---
title:  "A Programming Question on Frogs"
date:   2025-06-21
draft: false
tags:   
  - Programming
---
## Question

A frog is sitting at the bottom of a flight of 10 steps and scratching her head over how many ways she can jump up the stairs. She can jump 1, 2, or 3 steps at a time. For example, she can cover the 10 steps by jumping $(2,2,2,2,2),$ $(3,3,2,1,1)$ steps or other suitable combinations. Note that $(3,3,2,2)$ is distinct from $(2,2,3,3)$, and she only wants to find the number of possible solutions, not the exact solutions. Work out a function for the frog that solves this problem for any $n$ number of steps (not just 10).

## Algorithm

```
jump(n)
	if n = 1 then 1
	else if n = 2 then 2
	else if n = 3 then 4
	else jump(n-1) + jump(n-2) + jump(n-3)
```

## Proof of Correctness

Consider the function to be $\texttt{jump(n)}$.

Base Cases: For $n=1$, the frog can jump $1$ way $(1)$. For $n=2$, the frog can jump in $2$ ways $(1,1), (2)$. For $n=3$, it can jump in $4$ ways $(1,1,1), (1,2), (2,1), (3)$.

Induction Hypothesis: Assume that for $k$ steps, where $3 < k < n$, $\texttt{jump(k)}$ correctly computes the number of ways to jump $k$ steps.

Induction Step: For $k=n$ we show that $\texttt{jump(n)}$ is correct. For $\texttt{jump(n)}$ the frog can take either $1,2$ or $3$ steps hence 

$\texttt{jump(n)} = \texttt{jump(n-1)} + \texttt{jump(n - 2)} + \texttt{jump(n-3)}$ 

Since $\texttt{jump(n-1)}, \texttt{jump(n-2)}, \text{ and } \texttt{jump(n-3)}$ are in the range $3 < k < n$, $\texttt{jump(n)}$ must be true by induction hypothesis. Hence $\texttt{jump(n)}$ is proved to correctly computer the number of ways to jump $n$ steps by induction.


## Complexity

Each recursive call grows exponentially and since there are $3$ calls, the time and space complexity would be $O(3^n)$.
