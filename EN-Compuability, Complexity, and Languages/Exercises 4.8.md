# Exercises 4.8

## Problem 1

### Problem Description

Let $f(x_1,\ldots,x_n)$ be a function of $n$ variables, and let $f’(x)$ be a unary function defined so that $f’([x_1,\ldots,x_n])=f(x_1,\ldots,x_n)$ for all $x_1,\ldots,x_n$ and $f'(x)\uparrow$ if $Lt(x)>n$. Show that $f'$ is partially computable if and only if $f$ is partially computable.

### Solution

If $f'$ is partially computable as definition, then we can express $f$ as follow:

```c
Y <- f'([X,...,Xn])
```

If $f$ is partially computable as definition, then we can express $f’$ as follow:

```c
[A]	IF Lt(X) > n GOTO A
    Y <- f(x1(x),...,xn(x))
```

We view those primitive recursive function and their composition, recursion as macro for convenient. Where `xi(x)` represents $(x)_i$. 

## Problem 2

### Problem Description

Define $\text{Sort}([x_1,\ldots,x_n]-1)=[y_1,\ldots,y_n]-1$, where $n=\text{Lt}([x_1,\ldots,x_n])$ and $y_1,\ldots,y_n$ is a permutation of $x_1,\ldots,x_n$ such that $y_1\le y_2\le\cdots\le y_n$. Show that Sort($x$) is primitive recursive.

### Solution

First, define $g(y,x)$, where $x$ represents the parameter array and $y$ represents number of choices have been made. And
$$
g(0,x)=1\\
g(y+1,x)=g(y,x)*p^{y+1}_{\min_{t\le Lt(x)}(t\ne 0\;\&\;(g(y,x))_{t}=0\;\&\;(\forall j)_{\le Lt(x)}((g(y,x))_t\ne 0\lor (x)_t\le (x)_j))}
$$
Then, the Sort function can be expressed as
$$
\text{Sort}(x)=\prod_{i=1}^{\text{Lt}(x+1)}p_{(g(\text{Lt}(x+1),x+1))_i}^{(x+1)_i}-1
$$
which is primitive recursive.

## Problem 3

### Problem Description

Let $F(0)=0,F(1)=1,F(n+2)=F(n+1)+F(n)$. [$F(n)$ is the $n$th so-called Fibonacci number.] Prove that $F(n)$ is primitive recursive.

### Solution

Define function $G(x)$ s.t.
$$
G(0)=3\\
G(t+1)=2^{(G(t))_2}3^{(G(t))_1+(G(t))_2}
$$
Then
$$
F(x)=(G(x))_1
$$
Q.E.D.

## Problem 4

### Problem Description

(Simultaneous Recursion) Let
$$
h_1(x,0)=f_1(x),\\
h_2(x,0)=f_2(x),\\
h_1(x,t+1)=g_1(x,h_1(x,t),h_2(x,t)),\\
h_2(x,t+1)=g_2(x,h_1(x,t),h_2(x,t)).
$$
Prove that if $f_1,f_2,g_1,g_2$ all belong to some PRC class $\mathscr{C}$, then $h_1,h_2$ do also.

### Solution

Consider the following function $p(x,y)$
$$
p(x,0)=[f_1(x),f_2(x)]\\
p(x,t+1)=[g_1(x,(p(x,t))_1,(p(x,t))_2),g_2(x,(p(x,t))_1,(p(x,t))_2)]
$$
Thus, $p(x,y)$ belongs to $\mathscr{C}$, and so do $h_1,h_2$ because
$$
h_1(x,y)=(p(x,y))_1\\
h_2(x,y)=(p(x,y))_2
$$

## Problem 5

### Problem Description

(Course-of-Values Recursion)

(a) For $f(n)$ any function, we write
$$
\tilde{f}(0)=1,\tilde{f}(n)=[f(0),f(1),\ldots,f(n-1)]\text{ if }n\ne 0.
$$
Let
$$
f(n)=g(n,\tilde{f}(n))
$$
for all $n$. Show that if $g$ is primitive recursive so is $f$.

(b) Let
$$
f(0)=1,\quad f(1)=4,\quad f(2)=6,\\
f(x+3)=f(x)+f(x+1)^2+f(x+2)^3.
$$
Show that $f(x)$ is primitive recursive.

(c) Let
$$
h(0)=3\\
h(x+1)=\sum_{t=0}^xh(t).
$$
Show that $h$ is primitive recursive.

### Solution

#### a

Let $\beta(x)$ defined as
$$
\beta(0)=[g(0,1),1]\\
\beta(n+1)=[g(n+1,(\beta(n))_2*p_{n+1}^{(\beta(n))_1}),(\beta(n))_2*p_{n+1}^{(\beta(n))_1})]
$$
and $f(x)=(\beta(x))_1$, Q.E.D.

#### b

Observed that there is a function $k(x)$ such that
$$
k(0)=[1,4,6]\\
k(n+1)=[(k(n))_2,(k(n))_3,(k(n))_1+(k(n))_2^2+(k(n))_3^3]
$$
and then $f(n)=(k(n))_1$, thus it is primitive function.

#### c

We adapt a similar semantic for $\tilde h$ as $\tilde f$. Now we notice that
$$
h(t)=g(t,\tilde h(t))=\sum_{i=1}^t(\tilde h(t))_i
$$
when $t\ne 0$. Otherwise it would be $3$. So $h$ is primitive recursive directly from a).

## Problem 6

### Problem Description

(Unnested Double Recursion) Let
$$
f(0,y)=g_1(y)\\
f(x+1,0)=g_2(x)\\
f(x+1,y+1)=h(x,y,f(x,y+1),f(x+1,y)).
$$
Show that if $g_1,g_2$, and $h$ all belong to some PRC class $\mathscr{C}$, then $f$ also belongs to $\mathscr{C}$.

### Solution

Represent the function as $G$:
$$
f(x,y)=G(\frac{(x+y)(x+y+1)}{2}+x)
$$
Then we can represent $G(x)$ as:
$$
G(0)=g_1(0)\\
G(x+1)=\left\{\begin{array}{ll}
g_1(l),&n=0\\
g_2(l\dot-1)&n=l\;\&\;n>1\\
g_1(0)&n=l\;\&\;n=1\\
h(n\dot-1,l\dot-n\dot-1,G(\frac{(l\dot-1)l}{2}+n\dot-1),G(\frac{(l\dot-1)l}{2}+n))&\text{otherwise}
\end{array}\right.\\
\text{where }l=\min_{t\le x+1}(\frac{t(t+1)}{2}\le x+1)\text{ and }n=x+1\dot-\frac{l(l+1)}{2}
$$
From Problem 5 a), since $\frac{(l\dot-1)l}{2}+n<\frac{l(l+1)}{2}+l$ obviously hold for $n<l$, and that is the case for the fourth expression, we can use a similar $\tilde G$ to conclude that $G$ belongs to $\mathscr{C}$. And hence the $f(x,y)$ belongs to $\mathscr{C}$, too.
