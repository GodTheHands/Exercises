# Exercises 4.5

## Problem 1

### Problem Description

Let us call a predciate *trivial* if it is always TRUE or always FALSE. Show that no nontrivial predicates belong to COMP (see Execrise 4.10 for the definition of COMP.)

### Solution

Trivial predicates $P(x_1,\ldots,x_n)$ can be expressed as $n(u_1^n(x_1,\ldots,x_n))$ or $s(n(u_1^n(x_1,\ldots,x_n)))$.

Now assume there exists som nontrivial predicate $Q(x_1,\ldots,x_n)$ belongs to COMP. Then $Q(x_1\ldots,x_n)=k$ or $Q(x_1,\ldots,x_n)=x_i+k$. Since it is nontrivial so it can’t be the former form. Since the value of a predicate must be 0 or 1, so it can’t be the second form since $x_i=2$ will simply break this assumption.