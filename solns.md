---
layout: page
title: "HW2 Solns: CMPT231"
subtitle: "Lecture 2, ch4-5"
ext-js: "https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=AM_CHTML"
---

### HW2 Solutions (20pts)

+ (1) *(4pts)* Demonstrate **merge sort**:

  | p | r | A[0] | A[1] | A[2] | A[3] | A[4] | A[5] | A[6] | A[7] |
  |---|---|------|------|------|------|------|------|------|------|
  | 0 | 7 |  35  |  50  |  44  |  61  |  17  |  75  |  23  |   9  |
  | 0 | 3 |  35  |  50  |  44  |  61  |  --  |  --  |  --  |  --  |
  | 0 | 1 |  35  |  50  |  --  |  --  |  --  |  --  |  --  |  --  |
  | 2 | 3 |  --  |  --  |  44  |  61  |  --  |  --  |  --  |  --  |
  | 0 | 3 |  35  |  44  |  50  |  61  |  --  |  --  |  --  |  --  |
  | 4 | 7 |  --  |  --  |  --  |  --  |  17  |  75  |  23  |   9  |
  | 4 | 5 |  --  |  --  |  --  |  --  |  17  |  75  |  --  |  --  |
  | 6 | 7 |  --  |  --  |  --  |  --  |  --  |  --  |  23  |   9  |
  | 6 | 7 |  --  |  --  |  --  |  --  |  --  |  --  |   9  |  23  |
  | 4 | 7 |  --  |  --  |  --  |  --  |   9  |  17  |  23  |  75  |
  | 0 | 7 |   9  |  17  |  23  |  35  |  44  |  50  |  61  |  75  |

+ (2) Consider the recurrence: \` T(n) = T(n/2) + T(n/4) + O(n) \`.
  + a. *(3pts)* **Guess** a solution to the recurrence, showing your work.

    Drawing a recursion tree, we see that at each level of recursion,
    a total of \` c (3/4)^k n \` work is done.  There are a total of
    `lg(n)` levels of the tree.  So the total work is
    \` T(n) = n sum\_(k=0)^(text(lg) n) (3/4)^k \`.
    This is a geometric series, with solution
    \` T(n) = n ((1-(3/4)^(text(lg) n+1))/(1 - (3/4))) \`.
    This simplifies to
    \` T(n) = 4n ( 1 - (3/4)^(text(lg) n+1) ) \`.
    Since 3/4 &lt; 1, this is within O(n).
    Our guess is T(n) = O(n).
    (Contrast with merge sort, where the base of the exponential is 1, not 3/4.)

  + b. *(3pts)* **Prove** your guess to be correct.

    Proof by induction.
    Apply the inductive hypothesis at n/2 and n/4, and use the definition of O():

    \` exists n\_1, n\_2, n\_3, c\_1, c\_2, c\_3:
    forall n > text(max)(n\_1, n\_2, n\_3), \`

    \` T(n/2) <= c\_1 n/2 \`, \` T(n/4) <= c\_2 n/4 \`, and
    \` T(n) <= T(n/2) + T(n/4) + c\_3 n\`.

    So \` T(n) <= c\_1 n/2 + c\_2 n/4 + c\_3 n \`
    \` = (c\_1/2 + c\_2/4 + c\_3)n \`.

    So let \`n\_0 = text(max)(n\_1, n\_2, n\_3)\`
    and \` c\_0 = (c\_1/2 + c\_2/4 + c\_3)n \`.

    Then \` forall n > n\_0, T(n) <= c\_0 n \`, i.e., T(n) = O(n).

+ (3) *(3pts)* Solve the **recurrence**:
  \` T(n) = 8T(n/2) + 3n^3 + n^2 log n \`

  Master method, case 1:
  \` f(n) = 3n^3 + n^3 log n = Theta(n^3) = Theta(n^(log\_2 8)) = Theta(n^(log\_(b) a)) \`

+ (4) *(3pts)* Demonstrate **maximum subarray** on the following input:

  As in the textbook, we assume midpoints are calculated as *floor* of
  average of low and high. 

  |  l |  r | sum |  6 | -5 |  4 | -1 | -2 |  4 |  0 | -3 |  2 |  3 |
  |----|----|-----|----|----|----|----|----|----|----|----|----|----|
  |  1 |  1 |  6  |  6 | -5 | -- | -- | -- | -- | -- | -- | -- | -- |
  |  3 |  3 |  4  | -- | -- |  4 | -1 | -- | -- | -- | -- | -- | -- |
  |  3 |  3 |  4  | -- | -- |  4 | -1 | -2 | -- | -- | -- | -- | -- |
  |  1 |  1 |  6  |  6 | -5 |  4 | -1 | -2 | -- | -- | -- | -- | -- |
  |  6 |  6 |  4  | -- | -- | -- | -- | -- |  4 |  0 | -- | -- | -- |
  |  9 |  9 |  2  | -- | -- | -- | -- | -- | -- | -- | -3 |  2 | -- |
  |  9 | 10 |  5  | -- | -- | -- | -- | -- | -- | -- | -3 |  2 |  3 |
  |  6 | 10 |  6  | -- | -- | -- | -- | -- |  4 |  0 | -3 |  2 |  3 |
  |  1 | 10 |  8  |  6 | -5 |  4 | -1 | -2 |  4 |  0 | -3 |  2 |  3 |

+ (5) *(4pts)* **Randomised insertion sort**:

  Since the worst-case and average-case times for insertion sort were already
  the same \`(Theta(n^2))\`, the shuffle doesn't benefit us; there weren't any
  pathological corner cases to start with.
  And we lose the possiblity of verifying pre-sorted input in O(n) time.

            def shuffle(A):
              n = length(A)
              for i in 0 to n-1:
                swap( A[i], A[ random( i, n-1 ) ] )

            def rInsertSort(A):
              shuffle(A)
              n = length(A)
              for j = 1 to n-1:
                key = A[j]
                i = j-1
                while i >= 0 and A[i] > key:
                  A[ i+1 ] = A[ i ]
                  i = i-1
                A[ i+1 ] = key

