# Exercise 4.6

## Problem 1

### Problem Description

Let $f(x)=2x$ if $x$ is a perfect square; $f(x)=2x+1$ otherwise. Show that $f$ is primitive recursive.

### Solution

Observed that predicate
$$
PS(x)\Leftrightarrow(\exist t)_{\le x}(t*t=x)
$$
is primitive recursive. So is
$$
f(x)=\left\{\begin{array}{ll}2x,&PS(x)\\2x+1,&\text{otherwise}\end{array}\right.
$$

## Problem 2

### Problem Description

Let $\sigma(x)$ be the sum of the divisors of $x$ if $x\ne 0$; $\sigma(0)=0$ [e.g., $\sigma(6)=1+2+3+6=12$]. Show that $\sigma(x)$ is primitive recursive.

### Solution

Define $s(x,y)$ to be the sum of divisors of $x$ and smaller than $y$. Then
$$
s(x,y)=\sum_{t=1}^y(t|x)*t
$$
$s$ is primitive recursive, and $\sigma(x)=s(x,x)$. Then $\sigma$ is primitive recursive.

## Problem 3

### Problem Description

Let $\pi(x)$ be the number of primes that are $\le x$. Show that $\pi(x)$ is primitive recursive.

### Solution

We know
$$
\pi(x)=\sum_{i=1}^x\text{Prime}(i)
$$
and thus it is primitive recursive.

## Problem 4

### Problem Description

Let SQSM($x$) be true if $x$ is the sum of two perfect squares; false otherwise. Show that SQSM($x$) is primitive recursive.

### Solution

We know
$$
\text{SQSM}(x)=(\exist t)_{\le x}(PS(t)\land PS(x-t))
$$
The definition of $PS(\cdot)$ can be seen in Problem 1.

## Problem 5

### Problem Description

Let $\mathscr{C}$ be a PRC class, let $P(t,x_1,\ldots,x_n)$ be a predicate in $\mathscr{C}$, and let
$$
\begin{aligned}g(y,z,x_1,\ldots,x_n)&=(\forall t)_{y\leq t\leq z}P(t,x_1,\ldots,x_n)\mathrm{~and}\\h(y,z,x_1,\ldots,x_n)&=(\exists t)_{y\leq t\leq z}P(t,x_1,\ldots,x_n),\end{aligned}
$$
(where $(\forall t)_{y\le t\le z}P(t,x_1,\ldots,x_n)$ and $(\exist t)_{y\le t\le z}P(t,x_1,\ldots,x_n)$ mean that $P(t,x_1,\ldots,x_n)$ is true for all $t$ (respectively, for some $t$) from $y$ to $z$). Show that $g,h$ also belong to $\mathscr{C}$.

### Solution

From definition, when $y>z$ there’s no such a $t$ to determine whether $P(t,x_1,\ldots,x_n)$ is true. Thus we assume it would be false.

We denote such a predicate (obviously also in $\mathscr{C}$)
$$
Q(y,z,x_1,\ldots,x_n)=P(y+z,x_1,\ldots,x_n)
$$
WLOG, for $g(y,z,x_1,\ldots,x_n)$ we can derive
$$
g(y,z,x_1,\ldots.x_n)=(\forall t)_{t\le z\dot{-}y}Q(y,t,x_1,\ldots,x_n)
$$
the above equation holds when $y\le z$, so we can express $g$ as
$$
g(y,z,x_1,\ldots,x_n)=\left\{\begin{array}{ll}
0,&y>z\\
(\forall t)_{t\le z\dot{-}y}Q(y,t,x_1,\ldots,x_n),&\text{otherwise}
\end{array}\right.
$$
Now it is enough to say $g$ is in $\mathscr{C}$ since it is derived by $P$ and primitive recursive.

And from the same proof, we $h$ also belongs to $\mathscr{C}$.

## Problem 6

### Problem Description

Let RP($x,y$) be true if $x$ and $y$ are relatively prime (i.e., their greatest common divisor is 1). Show that RP($x,y$) is primitive recursive.

### Solution

Since $0$ can’t be relateively prime with any natural number, so we will define
$$
\text{RP}(x,y)=\left\{
\begin{array}{ll}
0,&x=0\lor y=0\\
\sim(\exist i)_{\le x}((\exist j)_{\le y}(i|x\land j|y\land i=j\land i\ne 1))&\text{otherwise}
\end{array}
\right.
$$

## Problem 7

### Problem Description

Give a sequence of compositions and recursions that shows explicitly that Prime($x$) is primitive recursive.

### Solution

Assume those functions appeared in textbook can be treat alternatively as their definition (other than Prime($x$), of course).
#### First Level Decomposition

From the expression of Prime($x$), we can directly decompose three functions: logic and, $x>1$ and $(\forall t)_{\le x}\{t=1\lor t=x\lor\sim(t|x)\}$.

#### Second Level Decomposition

##### $x>1$

From observation, $x>1$ is the composition of “>” operator, projection function $u_1^1(x)$ and $s(n(x))$(which represents 1).

##### $(\forall t)_{\le x}\{t=1\lor t=x\lor\sim(t|x)\}$

We can rewrite this predicate as
$$
\prod_{t=0}^x(t=1\lor t=x\lor\sim(t|x))
$$
is the composition of iterated production and $t=1\lor t=x\lor\sim(t|x)$.

#### Three Level Decomposition

We assume logic or is left associative. Then $t=1\lor t=x\lor\sim(t|x)$ is the composition of logic or and $t=1\lor t=x$ and $\sim(t|x)$.

The former, $t=1\lor t=x$ is the composition of logic or and $t=1$ and $t=x$, the composition of “=” operator, projection function and constant function (which can be further expressed as the composition of projection function and successor function) and the composition of “=” operator, projection functions.

The latter, $\sim(t|x)$ is the composition of operator “$\sim$” and $t|x$, where $t|x$ has already been defined.
