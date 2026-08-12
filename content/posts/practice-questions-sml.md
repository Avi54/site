---
title:  "Answers to Select Practice Programming Questions on SML"
date:   2025-06-23
draft: false
tags:   
  - Programming
---
The practice questions were taken from this [website](https://classes.engineering.wustl.edu/cse425s/index.php?title=SML_Practice_Problems_A).

### Q1
Write a function $\texttt{alternate : int list -> int}$ that takes a list of numbers and adds them with alternating sign. For example alternate $\texttt{[1,2,3,4] = 1 - 2 + 3 - 4 = -2}$. 

```
fun alternate(ls) = 
  let
    fun iter([],count,sum) = sum
      | iter(x::xs,count,sum) = 
        if (count mod 2 = 0) then iter(xs,count + 1,sum + x)
	else iter(xs,count + 1,sum - x)
  in
    iter(ls,0,0)
  end;
```

### Q2 
Write a function $\texttt{min\_max : int list -> int * int}$ that takes a non-empty list of numbers, and returns a pair $\texttt{(min, max)}$ of the minimum and maximum of the numbers in the list.

```
fun min\_max([]) = raise Fail "Empty list"
  | min\_max([x]) = (x, x)
  | min\_max(x::xs) = 
      let
        fun helper([], min, max) = (min, max)
          | helper(x::xs, min, max) = 
	      if (x > max) then helper(xs, min, x)
	      else if (x < min) then helper(xs, x, max)
	      else helper(xs, min, max)
      in
        helper(xs, x, x)
      end;
```

### Q3
Write a function $\texttt{cumsum : int list -> int list}$ that takes a list of numbers and returns a list of the partial sums of those numbers. For example cumsum $\texttt{[1,4,20] = [1,5,25]}$

```
fun cumsum(ls) = 
  let
    fun cumhelper([], p) = []
      | cumhelper(x::xs, p) = (x + p)::cumhelper(xs, x + p) 
  in
    cumhelper(ls, 0)
  end; 
```

### Q4
Write a function $\texttt{repeat : int list * int list -> int list}$ that given a list of integers and another list of nonnegative integers, repeats the integers in the first list according to the numbers indicated by the second list. For example: repeat ([1,2,3], [4,0,3]) = [1,1,1,1,3,3,3]

```
fun repeat([],[]) = []
  | repeat(x::xs, y::ys) = 
      let
        fun iter(x, 0) = []
          | iter(x, y) = x::iter(x, y -1)
      in
        iter(x, y)@repeat(xs, ys)
      end;
```

### Q5
Write a function $\texttt{any : bool list -> bool}$ that given a list of booleans returns true if there is at least one of them that is true, otherwise returns false. (If the list is empty it should return false because there is no true.)

```
fun any([]) = false
  | any(x::xs) = 
      if (x = true) then true
      else any(xs);
```

### Q6
Write a function $\texttt{all : bool list -> bool}$ that given a list of booleans returns true if all of them true, otherwise returns false. (If the list is empty it should return true because there is no false.)
```
fun all([]) = true
  | all(x::xs) = 
      if (x = false) then false
      else all(xs); 
```

### Q7
Write a function $\texttt{zip : int list * int list -> int * int}$ that given two lists of integers creates 
consecutive pairs, and stops when one of the lists is empty. 
For example: $\texttt{zip ([1,2,3], [4, 6]) = [(1,4), (2,6)]}$

```
fun zip([], _) = []
  | zip(_, []) = []
  | zip(x::xs, y::ys) = 
     (x,y)::zip(xs,ys);
```

### Q8
Write a version $\texttt{zipRecycle}$ of $\texttt{zip}$, where when one list is empty it starts recycling from its start until the other list completes. For example: $\texttt{zipRecycle ([1,2,3], [1, 2, 3, 4, 5, 6, 7]) = }$
$\texttt{[(1,1), (2,2), (3, 3), (1,4), (2,5), (3,6), (1,7)]}$

```
fun zipRecycle (l1, l2) =
  let
    fun recycle ([], ys) = recycle (l1, ys)
      | recycle (xs, []) = recycle (xs, l2)
      | recycle (x::xs, y::ys) = (x, y) :: recycle (xs, ys)
  in
    recycle (l1, l2)
  end;
```

### Q9
Write a function $\texttt{splitup : int list -> int list * int list}$ that given a list of integers creates two lists of integers, one containing the non-negative entries, the other containing the negative entries. Relative order must be preserved: All non-negative entries must appear in the same order in which they were on the original list, and similarly for the negative entries.

```
fun splitup(ls) =
  let
    fun rev(ls) =
      let
        fun helper([], r) = r
          | helper(x::xs, r) = helper(xs, x::r)
      in
        helper(ls, [])
      end

    fun iter([], p, n) = [rev(p), rev(n)]
      | iter(x::xs, p, n) =
          if x >= 0 then iter(xs, x::p, n)
          else iter(xs, p, x::n)
  in
    iter(ls, [], [])
  end;
```

### Q10
Write a version $\texttt{splitAt : int list * int -> int list * int list}$ of the previous function that takes an extra "threshold" parameter, and uses that instead of $0$ as the separating point for the two resulting lists. 

```
fun splitat(ls, pivot) =
  let
    fun rev(ls) =
      let
        fun helper([], r) = r
          | helper(x::xs, r) = helper(xs, x::r)
      in
        helper(ls, [])
      end

    fun iter([], p, n, pivot) = [rev(p), rev(n)]
      | iter(x::xs, p, n, pivot) =
          if (x >= pivot) then iter(xs, x::p, n, pivot)
          else iter(xs, p, x::n, pivot)
  in
    iter(ls, [], [], pivot)
  end;
```

### Q11
Write a function $\texttt{isAnySorted : int list -> boolean}$, that given a list of integers determines whether the list is sorted in either increasing or decreasing order. 

```
fun isAnySorted(ls) = 
  let
    fun asc([], prev) = true
      | asc(x::xs, prev) = 
          if (x >= prev) then asc(xs, x)
	  else false
    
    fun dsc([], prev) = true
      | dsc(x::xs, prev) = 
          if (x <= prev) then dsc(xs, x)
	  else false
  in
    if asc(ls, hd(ls)) then true
    else dsc(ls, hd(ls))
  end;
```

### Q12
Write a function $\texttt{sortedMerge : int list * int list -> int list}$ that takes two lists of integers that are each sorted from smallest to largest, and merges them into one sorted list. For example: $\texttt{sortedMerge ([1,4,7], [5,8,9]) = [1,4,5,7,8,9]}$.

```
fun sortedMerge([],l2) = l2
  | sortedMerge(l1,[]) = l1
  | sortedMerge(x::xs, y::ys) = 
      if (x <= y) then x::sortedMerge(xs, y::ys)
      else y::sortedMerge(x::xs, ys);
```

### Q13
Write a sorting function $\texttt{qsort : int list -> int list}$ that works as follows: Takes the first element out, and uses it as the "threshold" for $\texttt{splitAt}$. It then recursively sorts the two lists produced by $\texttt{splitAt}$. Finally it brings the two lists together. (Don't forget that element you took out, it needs to get back in at some point). You could use sortedMerge for the "bring together" part, but you do not need to as all the numbers in one list are less than all the numbers in the other.

```
fun qsort([]) = []
  | qsort(p::xs) = 
      let
        fun split([], l, r) = (l, r)
	  | split(x::xs, l, r) = 
	      if (x <= p) then split(xs, x::l, r)
	      else split(xs, l, x::r)

        val (l, r) = split(xs, [], [])
      in
        qsort(l) @ [p] @ qsort(r)
      end;
```

