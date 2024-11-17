# Exercises 4.7

## Problem 1

### Problem Description

Let $h(x)$ be the integer $n$ such that $n\le\sqrt{2}x<n+1$. Show that $h(x)$ is primitive recursive.

### Solution

Notice the inequality is indeed
$$
n^2\le 2x^2<(n+1)^2
$$
and combine with the fact
$$
\sqrt{2}x\le 2x
$$
Then we can express $h(x)$ as
$$
h(x)=\min_{t\le 2x}(n^2\le 2x^2\;\&\;2x^2<(n+1)^2)
$$
Note that power function, inequality, and minimalization function is primitive recursive. So is $h(x)$.

## Problem 2

### Problem Description

Do the same when $h(x)$ is the integer $n$ such that
$$
n\le(1+\sqrt{2})x<n+1.
$$


### Solution

To remove the annoying $\sqrt2$, we need to minus $x$ in both side. However the condition for $n<x$ should be cared.

Note that it is impossible for any $n<x$ to satisfy the inequality. Since if $x=0$ there’s impossible to find $n<x$, however if not, the inequality becomes
$$
(1+\sqrt{2})x<n+1<x+1
$$
 which indicates
$$
\sqrt{2}x<1
$$
a contradiction when $x\ge 1$. So we now can claim
$$
(n\dot{-}x)^2\le 2x^2<(n+1\dot{-}x)^2
$$
If we take the view of $n\dot{-}x$, it is totally the same as Problem 1, and by the constraint we can confidently assure current $h(x)$ is just the previous $h(x)$ in Problem 1 add $x$.

## Problem 3

### Problem Description

$p$ is called a *larger twin prime* if $p$ and $p-2$ are both pimes. (5, 7, 13, 19 are larger twim primes.) Let $T(0)=0$, $T(n)=$ the $n$th larger twin prime. It is widely believed, but has not been proved, that there are infinitely many larger twin primes. Assuming that this is true prove that $T(n)$ is computable.

### Solution

Consider the recursive equation
$$
T(0)=0\\
T(n+1)=\min_y(\text{Prime}(y)\;\&\;\text{Prime}(y\dot{-}2)\;\&\;y>T(n))
$$
Though $\min_y$ may be partially computable, we assume there’s infinite larger twin primes, so there will always be such a $y$ satisfy the predicate in $min_y$. Otherwise such an upper bound will reach the conclusion that larger twim primes are finite. So this is computable.

## Problem 4

### Problem Description

Let $u(n)$ be the $n$th number in order of size which is the sum of two squares. Show that $u(n)$ is primitive recursive.

### Solution

By observation, an upper bound for $u(n)$ is $2n^2$, since there will be at least $n+1$ such numbers $2*0^2,2*1^2,\cdots,2*(n-1)^2,2n^2$ satisfy the predicate. So we can define such a recursive equation
$$
u(0)=0\\
u(n+1)=\min_{y\le 2(n+1)^2}(SQSM(y)\;\&\;y>u(n))
$$
Check Exercises 4.6 Problem 4 for the definition of SQSM.

## Problem 5

### Problem Description

Let $R(x,t)$ be a primitive recursive predicate. Let
$$
g(x,y)=\max_{t\le y}R(x,t),
$$
i.e., $g(x,y)$ is the largest value of $t\le y$ for which $R(x,t)$ is true; if there is none, $g(x,y)=0$. Prove that $g(x,y)$ is primitive recursive.

### Solution

Consider about the primitive recursive function
$$
R'(x,y,z)=R(x,y\dot{-}z)
$$
Then we know
$$
g(x,y)=\max_{t\le y}R(x,t)=\min_{t\le y}R'(x,y,t)
$$
Hence it is proved.

## Problem 6

### Problem Description

Let gcd($x,y$) be the greatest common divisor of $x$ and $y$. Show that gcd($x,y$) is a primitive recursive.

### Solution

We assume that if such a common divisor does not exist, gcd($x,y$)$=0$ (such a condition happens if and only if $x$ or $y$ equals 0).

By observation, an upper bound is $x+y$, so we can define
$$
\text{gcd}(x,y)=\max_{t\le x+y}(t\;|\;x\;\&\;t\;|\;y)
$$
Hence, it is proved.

## Problem 7

### Problem Description

Let lcm($x,y$) be the least common multiple of $x$ and $y$. Show that lcm($x,y$) is primitive recursive.

### Solution

If gcd($x,y$)$=0$, we would infer $x$ or $y$ or both are $0$. In this case we will claim lcm($x,y$)$=0$. Then
$$
\textit{lcm}(x,y)=\lfloor (xy)/(\text{gcd}(x,y))\rfloor
$$
Hence, it is proved.

## Problem 8

### Problem Description

Give a computable predicate $P(x_1,\ldots,x_n,y)$ such that the function $\min_y P(x_1,\ldots,x_n,y)$ is not computable.

### Solution

Consider
$$
P(x)=(x+1)\;|\;x
$$
This is impossible and will lead to undefined value.

## Problem 9

### Problem Description

A function is *elementary* if it can be obtained from the functions $s,n,u_j^i,+,\dot{-}$ by a finite sequence of applications of composition, bounded summation, and bounded product. (By application of bounded summation we mean obtaining the function $\sum_{t=0}^yf(t,x_1,\ldots,x_n)$ from $f(t,x_1,\ldots,x_n)$, and similarly for bounded product.)

(a) Show that every elementary function is primitive recursive.

(b) Show that $x\cdot y,x^y$, and $x!$ are elementary.

(c) Show that if $n+1$-ary predicates $P$ and $Q$ are elementary, then so are $\sim P,P\lor Q,P\;\&\;Q,(\forall t)_{\le y}P(t,x_1,\ldots,x_n),(\exists t)_{\le y}P(t,x_1,\ldots,x_n)$, and $\min_{t\le y}P(t,x_1,\ldots,x_n)$.

(d) Show that Prime($x$) is elementary.

(e) Let the binary function $\exp_y(x)$ be defined
$$
\exp_0(x)=x\\
exp_{y+1}(x)=2^{\exp_y(x)}
$$
Show that for every elementary function $f(x_1,\ldots,x_n)$, there is a constant $k$ such that $f(x_1,\ldots,x_n)\le\exp_k(\max\{x_1,\ldots,x_n\})$. [Hint: Show that for every $n$ there is an $m\ge n$ such that $x\cdot\exp_n(x)\le\exp_m(x)$ for all $x$.]

(f) Show that $\exp_y(x)$ is not elementary. Conclude that the class of elementary functions is a proper subset of the class of primitive recursive functions.

### Solution

#### (a)

From all the derivation in textbook, we know that all operation here is some kind of primitive recursion. So this is obvious.

#### (b)

For $x\cdot y$, we can express it as
$$
\sum_{t=0}^yx\dot{-}x
$$
We should show the following two function is elementary:
$$
\alpha(x)=1\dot{-}x\\
\beta(x)=1\dot{-}\alpha(x)
$$
For $x^y$, we can express it as
$$
\beta(y)\cdot\sum_{t=0}^{y\dot{-}1}x+\alpha(y)
$$
For $x!$, we can express it as
$$
\prod_{t=0}^{y\dot{-}1}(t+1)
$$
Hence (b) is proved.

#### (c)

We know
$$
\sim P=\alpha(P)\\
P\lor Q=P\cdot Q\\
P\;\&\;Q=\sim(\sim P\lor \sim Q)\\
(\forall t)_{\le y}P(t,x_1,\ldots,x_n)=\prod_{t=0}^yP(t,x_1,\ldots,x_n)\\
(\exists t)_{\le y}P(t,x_1,\ldots,x_n)=\beta(\sum_{t=0}^yP(t,x_1,\ldots,x_n))\\
\min_{t\le y}P(t,x_1,\ldots,x_n)=\sum_{t=0}^y\prod_{r=0}^t\alpha(P(r,x_1,\ldots,x_n))
$$
Obviously these are elementary.

#### (d)

Since
$$
|x-y|=(x\dot{-}y)+(y\dot{-}x)\\
x=y\Leftrightarrow \alpha(|x-y|)\\
y\;|\;x\Leftrightarrow(\exists t)_{\le x}(y\cdot t=x)\\
x>y\Leftrightarrow\beta(x\dot{-}y)\\
\text{Prime}(x)\Leftrightarrow x>1\;\&\;(\forall t)_{\le x}(t=1\lor t=x\lor\sim(t\;|\;x))
$$
Q.E.D.

#### (e)

When $\max\{x_1,\ldots,x_n\}\ge 2$, assume after applying $k$ times of compositions, bounded summations or bounded productions will yield a class of functions with upper bound $U\ge 2$. Then for $k+1$ times, the upper bound should be
$$
\max\{\max\{x_1,\ldots,x_n\}U+U,U^{\max\{x_1,\ldots,x_n\}}*U\}=U*U^{\max\{x_1,\ldots,x_n\}}
$$
For $k=0$, the upper bound is
$$
\max\{x_1,\ldots,x_n\}+1
$$
So, for $f(x_1,\ldots,x_n)$, there should be some constant $l$, which indicates the application times of compositions, bounded summations and bounded productions. Basically, we can assume
$$
x\cdot\exp_k(x)<\exp_{k+2}(x)
$$
Here, when $k=0$, $x^2<2^{2^{x}}$ obviously hold. Then, when $k>0$, because
$$
x=\exp_0(x)<\exp_1(x)<\cdots<\exp_{n}(x)<\cdots
$$
then since when $x=0,1$ the inequality will always hold, then for $x>1$
$$
x\cdot\exp_{k+1}(x)=x\cdot 2^{\exp_{k}(x)}<2^{\exp_{k}(x)+x}<2^{x\cdot\exp_k(x)}<\exp_{k+3}(x)
$$
Now, consider the upper bound of $f$, we should note
$$
\max\{x_1,\ldots,x_n\}+1<2^{\max\{x_1,\ldots,x_n\}}\\
(\max\{x_1,\ldots,x_n\}+1)^{\max\{x_1,\ldots,x_n\}+1}<2^{\max\{x_1,\ldots,x_n\}2^{\max\{x_1,\ldots,x_n\}}}<2^{\exp_{3}(\max\{x_1,\ldots,x_n\})}\\
(\max\{x_1,\ldots,x_n\}+1)^{(\max\{x_1,\ldots,x_n\})^{\max\{x_1,\ldots,x_n\}+1}}<2^{\max\{x_1,\ldots,x_n\}2^{\exp_3(\max\{x_1,\ldots,x_n\})}}<2^{\exp_5(\max\{x_1,\ldots,x_n\})}\\
...
$$
Since we know the upper bound of $f$ is indeed the power tower of $(\max\{x_1,\ldots,x_n\})+1$ with $k+1$ layers. So it should be smaller than
$$
\exp_{2k+2}(\max\{x_1,\ldots,x_n\})
$$
Notice when $\max\{x_1,\ldots,x_n\}\le 1$, we can directly derive the upper bound with the similar statement.

Thus, the problem has been showed.

#### (f)

If $\exp_y(x)$ is elementary, it means there exist a constant $k$ that
$$
\exp_y(x)\le \exp_k(x)
$$
However if we let $y=k+1$, it leads
$$
\exp_{k+1}(x)\le \exp_k(x)\\
\exp_{k+1}(x)>\exp_k(x)
$$
So, $\exp_y(x)$ is not elementary. However it is obviously primitive recursive. Q.E.D.
