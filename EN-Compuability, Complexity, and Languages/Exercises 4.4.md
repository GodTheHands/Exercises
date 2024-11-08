# Exercises 4.3

## Problem 1

### Problem Description

Give a detailed argument that $x^y$, $p(x)$, and $x\dot{-}y$ are primitive recursive.

### Solution

Let $f_1(x,y)=x^y$, consider the following recurison equations:
$$
\begin{aligned}f_1(x,0)&=F_1(x)\\f_1(x,y+1)&=G_1(y,f_1(x,y),x)\end{aligned}
$$
and
$$
\begin{aligned}&F_1(x)=1\\&G_1(y,f_1(x,y),x)=f_1(x,y)\cdot x\Rightarrow G_1(x_1,x_2,x_3)=u^3_2(x_1,x_2,x_3)\cdot u^3_3(x_1,x_2,x_3)\end{aligned}
$$
Note that a function always equals to some constant is always primitive recursive since they can be expressed by composition of projection, zero and successor functions. Hence, $f_1$ is primitive recursive.

------

Let $f_2(x)=p(x)$, consider the following recurison equations:
$$
\begin{aligned}f_2(0)&=F_2\\f_2(y+1)&=G_2(y,f_2(y))\end{aligned}
$$
and
$$
\begin{aligned}&F_2=0\\&G_2(y,f_2(y))=y\Rightarrow G(x_1,x_2)=u^2_1(x_1,x_2)\end{aligned}
$$
Hence $f_2$ is primitive recursive.

---

Let $f_3(x,y)=x\dot{-}y$, consider the following recursion equations:
$$
\begin{aligned}f_3(x,0)&=F_3(x)\\f_3(x,y+1)&=G_3(y,f_3(x,y),x)\end{aligned}
$$
where
$$
\begin{aligned}&F_3(x)=x=u^1_1(x)\\&G(y,f_3(x,y),x)=p(f_3(x,y))\end{aligned}
$$
Hence $f_3$ is primitive recursive.

## Problem 2

### Problem Description

Show that for each $k$, the function $f(x)=k$ is primitive recursive.

### Solution

Since $f(x)$ can be constructed by first composite $s$ with $n$ as $c_1(x)=s(n(x))$. Hence, the $c_1$ is primitive recursive function, then we have primitive recursive function $c_2(x)=s(c_1(x))$, which always equals to $2$. We can repeat this approach until we get $c_k$, which represents the function $c_k(x)=k$, an alias of $f$.

## Problem 3

### Problem Description

Prove that if $f(x)$ and $g(x)$ are primitive recursive functions, so is $f(x)+g(x)$.

### Solution

$f(x)+g(x)$ is composition of $f(x)$, $g(x)$, and $h(x,y)=x+y$. These functions are all primitive recursive.

## Problem 4

### Problem Description

Without using $x+y$ as a macro, apply the constructions in the proofs of Theorems 1.1, 2.2, and 3.1 to give an $\mathscr{P}$ program that computes $x\cdot y$.

### Solution

> [!NOTE]
>
> If $h$ is obtained from the (partially) computable functions $f,g_1,\ldots,g_k$ by composition. Then the following program obviously computes $h$:
>
> ```pseudocode
> Z_1 <- g_1(X_1,...,X_n)
> ...
> Z_k <- g_k(X_1,...,X_n)
> Y <- f(Z_1,...,Z_k)
> ```
>
> If $h$ is obtained from $f$ and $g$ by recursion and let $f$, $g$ be computable. Then the following program computes $h$:
>
> ```pseudocode
> 	Y <- f(X_1,...X_n)
> [A]	IF X_{n+1} = 0 GOTO E
> 	Y <- g(Z,Y,X_1,...,X_n)
> 	Z <- Z + 1
> 	X_{n+1} <- X_{n+1} - 1
> 	GOTO A
> ```
>
> $s(x)=x+1$ is computed by
>
> ```pseudocode
> Y <- X + 1
> ```
>
> $u_i^n(x_1,...,x_n)$ is computed by the program
>
> ```pseudocode
> Y <- X_i
> ```
>
> $n(x)=0$ just represents the empty program.

First, consider recursive equations of $h(x,y)=x\cdot y$:
$$
\begin{aligned}h(x,0)&=n(x)\\h(x,y+1)&=g(y,h(x,y),x)\end{aligned}
$$
where $g(x_1,x_2,x_3)=f(u_2^3(x_1,x_2,x_3),u_3^3(x_1,x_2,x_3))$ and
$$
\begin{aligned}f(x,0)&=u_1^1(x)\\f(x,y+1)&=g_2(y,h(x,y),x)\end{aligned}
$$
where $g_2(x_1,x_2,x_3)=s(u_2^3(x_1,x_2,x_3))$.

So $g_2$ should have the form

```pseudocode
Z_1 <- u_2^3(X_1,X_2,X_3)
Y <- s(Z_1)
```

Since $s$ won’t change the value of input variables and the inside $Y$ won’t be affected by initial value of $Y$. So we can simplify $g_2$ as

```pseudocode
Y <- X_2 + 1
```

Then $f$ should have the form

```pseudocode
	Y <- f(X_1)
[A]	IF X_2 = 0 GOTO E
	Y <- g_2(Z,Y,X_1)
	Z <- Z + 1
	X_2 <- X_2 - 1
	GOTO A
```

The first line can be translated into `Y <- X_1`. Since $g_2$ won’t change the value of input variables, and the inside $Y$ won’t be affected by initial value of $Y$. So we can simplify $f$ as (eliminate $Z$ that haven’t been used):

```pseudocode
	Y <- X_1
[A] IF X_2 = 0 GOTO E
	Y <- Y + 1
	X_2 <- X_2 - 1
	GOTO A
```

$g$ should have the form

```pseudocode
Z_1 <- u_2^3(X_1,X_2,X_3)
Z_2 <- u_3^3(X_1,X_2,X_3)
Y <- f(Z_1,Z_2)
```

$f$ won’t change the value of $Z_1$, but it does to $Z_2$, and the inside $Y$ won’t be affected by initial value of $Y$. So we need to keep $Z_2$ (free to rename) as

```pseudocode
Z <- X_3
Y <- f(X_2,Z)
```

And then expand it

```pseudocode
	Z <- X_3
	Y <- X_2
[A] IF Z = 0 GOTO E
	Y <- Y + 1
	Z <- Z - 1
	GOTO A
```

$h$ should have the form:

```pseudocode
	Y <- n(X_1)
[A]	IF X_2 = 0 GOTO E
	Y <- g(Z,Y,X_1)
	Z <- Z + 1
	X_2 <- X_2 - 1
	GOTO A
```

This is the main program, so we assume `Y <- 0` is included implicitly and eliminate repeat statements. Renaming variables and labels:

```pseudocode
[A_2]	IF X_2 = 0 GOTO E_2
		Z <- X_1
[A]		IF Z = 0 GOTO E
		Y <- Y + 1
		Z <- Z - 1
		GOTO A
[E]		X_2 <- X_2 - 1
		GOTO A_2
```

Here, we discarded those redundant instruction such as assignment to the variable itself and never used variables.

## Problem 5

### Problem Description

For any unary function $f(x)$, the $n$th *iteration* of $f$, written $f^n$, is
$$
f^n(x)=f(\cdots f(x)\cdots),
$$
where $f$ is composed with itself $n$ times on the right side of the equation. (Note that $f^0(x)=x$.) Let $\iota_f(n,x)=f^n(x)$. Show that if $f$ is primitive recursive, then $\iota_f$ is also primitive recursive.

### Solution

Consider the recursive equations of $\iota_f$:
$$
\iota_f(0,x)=x=u_1^1(x)=F(x)\\
\iota_f(n+1,x)=f(\iota_f(n,x))=G(n,\iota_f(n,x),x)
$$
where
$$
G(x_1,x_2,x_3)=f(u_2^3(x_1,x_2,x_3))
$$
## Problem 6

### Problem Description

(a) Let $E(x)=0$ if $x$ is even, $E(x)=1$ if $x$ is odd. Show that $E(x)$ is primitive recursive.

(b) Let $H(x)=x/2$ if $x$ is even, $(x-1)/2$ if $x$ is odd. Show that $H(x)$ is primitive recursive.

### Solution

(a) Consider recursive equations:
$$
E(0)=0\\
E(t+1)=1\dot{-}E(t)=G(t,E(t))
$$
and
$$
G(x_1,x_2)=\alpha(u_2^2(x_1,x_2))
$$
(b) Consider recursive equations:
$$
H(0)=0\\
H(t+1)=H(t)+E(t)=H(t,H(t))
$$
and
$$
H(x_1,x_2)=u_2^2(x_1,x_2)+E(u_2^1(x_1,x_2))
$$
## Problem 7

### Problem Description

Let $f(0)=0$, $f(1)=1$, $f(2)=2^2$, $f(3)=3^{3^3}=3^{27}$, etc. In general, $f(n)$ is written as a stack $n$ high, of $n$’s as exponents. Show that $f$ is primitive recursive.

### Solution

Let $h(x,y)$ denotes stack $y$ high, of $x$’s as exponents, then $f(x)=h(x,x)$. And
$$
h(x,0)=1\dot{-}\alpha(x)\\
h(x,y+1)=x^{h(x,y)}
$$

## Problem 8

### Problem Description

Let $k$ be some fixed number, let $f$ be a function such that $f(x+1)<x+1$ for all $x$, and let
$$
\begin{aligned}h(0)&=k\\h(t+1)&=g(h(f(t+1))).\end{aligned}
$$
Show that if $f$ and $g$ belong to some PRC class $\mathscr{C}$, then so does $h$. [Hint: Define $f'(x)=\min_{l\le x}f^l(x)=0$]. See Exercise 5 for the definition of $f^l(x).$]

### Solution

Since
$$
h(t+1)=g(h(f(t+1)))=g(g(h(f(f(t+1)))))=g^2(h(f^2(t+1)))\cdots
$$
then
$$
h(t+1)=g^n(h(f^n(t+1)))\quad\text{for any }n\in N
$$
Note that $f(x+1)<x+1$, which means $f^n(x+1)$ will ultimately reach $0$ for $n\le x+1$. However, we don’t know the value of $f(0)$ at all, so it is helpful to define  $f’(x)=\min_{l\le x}f^l(x)=0$. Thus

$$
h(t+1)=g^{f'(t+1)}(h(f^{f'(t+1)}(t+1)))=g^{f'(t+1)}(k)
$$
We observed that $f'(0)=0$ must be true and $h(0)=g^{f'(0)}(k)=k$. So we can now express $h$ as:
$$
h(t)=g^{f'(t)}(k)=\iota_g(f'(t),k)
$$
Let $r(x,y)=\min_{0\le l\le y}\{f^l(x)\}$, so:
$$
r(x,0)=f^0(x)=x\\
r(x,y+1)=\min\{r(x,y),f^{y+1}(x)\}
$$
Let $\beta(x)=1-\alpha(x)$, we know $\beta$ is primitive recursive. Then we can define $min(x,y)$ as
$$
min(x,y)=\beta(x+1\dot{-}y)*x+\beta(y\dot{-}x)*y
$$
Then $min(x,y)$ is primitive recursive, and it must be in $\mathscr{C}$, so is $r(x,y)$. Define $s(x,y)$ is the smallest $0\le l\le y$ for $f^l(x)=0$, if such a $l$ doesn’t exist then equals to $y$. Hence, $s(x,x)=f'(x)$ and
$$
s(x,0)=\beta(x)\\
s(x,y+1)=s(x,y)+\beta(r(x,y)*f^y(x))
$$
prove that $s$ and $f’$ is in $\mathscr{C}$. Then so is $h$.

## Problem 9

### Problem Description

Let $g(x)$ be a primitive recursive function and let $f(0,x)=g(x)$, $f(n+1,x)=f(n,f(n,x))$. Prove that $f(n,x)$ is primitive recursive.

### Solution

We can make the hypothesis: $f(n,x)=g^{2^n}(x)$. Firstly, for $n=0$, $g(x)=g^{2^0}(x)$.

For $n=k+1$, $f(k+1,x)=f(k,f(k,x))=f(k,g^{2^k}(x))=g^{2^k}(g^{2^k}(x))=g^{2^{k+1}}(x)$, so hypothesis is true.

Because iteration of power is primitive recursive. So the $f(n,x)$ is just a composition of primitive recursive.

## Problem 10

### Problem Description

Let COMP be the class of functions obtained from the initial functions by a finite sequence of compositions.

(a) Show that for every function $f(x_1,\ldots,x_n)$ in COMP, either $f(x_1,\ldots,x_n)=k$ for some constant $k$, or $f(x_1,\ldots,x_n)=x_i+k$ for some $1\le i\le n$ and some constant $k$.

(b) An $n$-ary function $f$ is *monotone* if for all n-tuples $(x_1,\ldots,x_n)$, $(y_1,\ldots,y_n)$ such that $x_i\le y_i$, $1\le i\le n$, $f(x_1,\ldots,x_n)\le f(y_1,\ldots,y_n)$. Show that every function in COMP is monotone.

(c) Show that COMP is a proper subset of the class of primitive recursive functions.

(d) Show that the class of functions computed by straightline $\mathscr{P}$ programs is a proper subset of COMP. [See Exercise 4.6 in Chapter 2 for the definition of straightline programs.]

### Solution

(a) All such function can be categorized by composition level. For level 0, there are only three initial functions. For projection function we have $f(x_1,\ldots,x_n)=x_i$, where $k=0$. The other two functions are only available when $n=1$, $s(x)=x+1$ and $n(x)=0$ corresponds to the condition where $k=1$ and $k=0$ of two form.

Assume for function of composition level $l$ this holds, then for level $l+1$. If the outmost function is a projection, it produces just the parameter whose composition level must be $\le 1$ and also in COMP. So in this condition this also holds. The result is trivial when outmost function is zero function, and for the outmost function is sucessor function. There must be only one function as parameter, and be of form $k$ or $x_i+k$, by replacing $k$ with $k+1$ we proved this also holds with sucessor function.

(b) When $f(x_1,\ldots,x_n)=k$, it is obvious. When $f(x_1,\ldots,x_n)=x_i+k$ for some $1\le i\le n$, for every two tuples $(x_1,\ldots,x_n)$ and $(y_1,\ldots,y_n)$ where $x_j\le y_j$ for $1\le j\le n$. Then $f(x_1,\ldots,x_n)=x_i+k\le y_i+k=f(y_1,\ldots,y_n)$. Thus, COMP is monotone.

(c) COMP is obviously subset of primitive recursive functions. Consider $f(x,y)=x+y$, this is not in COMP but is primitive recursive.

(d) 

> [!NOTE]
>
> An $\mathscr{P}$ program is called a *straightline program* if it contains no (labeled or unlabeled) instruction of the form IF $V\ne 0$ GOTO $L$.

We have shown that $\psi_{\mathscr{P}}(x_1,\ldots,x_n)\le k$, where $k$ is some constant, since a function in COMP of the form $f(x_1,\ldots,x_n)=x_i+k+1$ for some $1\le i\le n$ will violate this constraint. So there is a program is COMP but not straightline.

Then, for a straightline program, we must run the program line by line. Since $Y$’s initial value is $0$, and we will retrieve $Y\leftarrow Y+1$ and $Y\leftarrow 0$ the same time (These are the only functions that would modify the value of $Y$). Then straightline program must be in COMP.

From above argument, the straightline program is a proper subset of COMP.

## Problem 11

### Problem Description

Let $\mathscr{P}_1$ be the class of all functions obtained from the initial functions by any finite number of compositions and no more than one recursion (in any order).

(a) Let $f(x_1,\ldots,x_n)$ belong to COMP. [See Exercise 10 for the definition of COMP.] Show that there is a $k>0$ such that $f(x_1,\ldots,x_n)\le\max\{x_1,\ldots,x_n\}+k$.

(b) Let
$$
\begin{aligned}h(0)&=c\\h(t+1)&=g(t,h(t)),\end{aligned}
$$
where $c$ is some given number and $g$ belongs to COMP. Show that there is a $k>0$ such that $h(t)\le tk+c$.

(c) Let
$$
\begin{aligned}h(x_1,\ldots,x_n,0)&=f(x_1,\ldots,x_n)\\h(x_1,\ldots,x_n,t+1)&=g(t,h(x_1,\ldots,x_n,t),x_1,\ldots,x_n),\end{aligned}
$$
where $f$, $g$ belong to COMP. Show that there are $k,l>0$ such that $h(x_1,\ldots,x_n,t)\le tk+\max\{x_1,\ldots,x_n\}+l$.

(d) Let $f(x_1,\ldots,x_n)$ belong to $\mathscr{P}_1$. Show that there are $k,l>0$ such that $f(x_1,\ldots,x_n)\le\max\{x_1,\ldots,x_n\}\cdot k+l$.

(e) Show that $\mathscr{P}_1$ is a proper subset of the class of primitive recursive functions.

### Solution

(a) From Problem 10, we know that for every function $f(x_1,\ldots,x_n)$ in COMP, either $f(x_1,\ldots,x_n)=k$ for some constant $k$, or $f(x_1,\ldots,x_n)=x_i+k$ for some $1\le i\le n$ and some constant $k$. For all cases, we can take $k'=k+1$. Then we have
$$
f(x_1,\ldots,x_n)\le k\le\max\{x_1,\ldots,x_n\}+k'
$$
or
$$
f(x_1,\ldots,x_n)\le x_i+k\le \max\{x_1,\ldots,x_n\}+k'
$$
where $k'\ge 1$.

(b) From (a), we know
$$
h(t+1)\le\max\{t,h(t)\}+k\le\max\{t,\max\{t-1,h(t-1)\}+k\}+k=\max\{t,t+k-1,h(t-1+k)\}+k
$$
Since $t+k-1\ge t$, then
$$
\max\{t,t+k-1,h(t-1+k)\}+k=\max\{t+k-1,h(t-1)+k\}+k=\max\{t-1,h(t-1)\}+2k
$$
We can repeat above approach, until we get
$$
h(t+1)\le\max\{0,h(0)\}+(t+1)k=c+(t+1)k
$$
Which implies for $t\ge 1$, $h(t)\le c+tk$. For $t=0$, $h(t)\le c$ always hold.

(c) Similar to (b), we can do the following:
$$
\begin{aligned}
h(x_1,\ldots,x_n,t+1)&\le \max\{t,h(x_1,\ldots,x_n,t),x_1,\ldots,x_n\}+k\\
&=\max\{t,\max\{t-1,h(x_1,\ldots,x_n,t-1),x_1,\ldots,x_n\}+k,x_1,\ldots,x_n\}+k\\
&=\max\{t,t+k-1,h(x_1,\ldots.x_n,t-1)+k,x_1+k,\ldots,x_n+k,x_1,\ldots,x_n\}\\
&=\max\{t+k-1,h(x_1,\ldots,x_n,t-1)+k,x_1+k,\ldots,x_n+k\}\\
&=\max\{t-1,h(x_1,\ldots,x_n,t-1),x_1,\ldots,x_n\}+k\\
&\le\max\{0,h(x_1,\ldots,x_n,0),x_1,\ldots,x_n\}+(t+1)k\\
&=\max\{f(x_1,\ldots,x_n),x_1,\ldots x_n\}+(t+1)k
\end{aligned}
$$
Since $f$ is in COMP, so there is a constant $l$ that
$$
f(x_1,\ldots,x_n)\le\max\{x_1,\ldots,x_n\}+l
$$
Hence
$$
\begin{aligned}
h(x_1,\ldots,x_n,t+1)&\le \max\{x_1,\ldots,x_n\}+l+(t+1)k
\end{aligned}
$$
Hence, for $t\ge 1$, we have $h(x_1,\ldots,x_n,t)\le\max\{x_1,\ldots,x_n\}+l+tk$, when $t=0$, the target inequality becomes $f(x_1,\ldots,x_n)\le\max\{x_1,\ldots,x_n\}+l$, which is naturally held.

(d) Firstly, assume $f$ itself is a recursion. WLOG, we assume $x_n$ is the variable introduced by recursion. So from (c) we have
$$
f(x_1,\ldots,x_n)\le x_nk+\max\{x_1,\ldots,x_{n-1}\}+l\le x_nk+k\max\{x_1,\ldots,x_{n-1}\}+l=k\cdot\max\{x_1,\ldots,x_n\}+l
$$
Here we ignore the case $f$ is in COMP, because the conclusion is obvious.

Now consider $f$ itself is not defined by recursion, but it contains some function $g$ defined by recursion. Then we see the $g$ itself as a input variable (i.e., with the same status as $x_i$). Then we just extend the $f$ and get $f(x_1,\ldots,x_n,g)$ and $f$ now satisfy $f(x_1,\ldots,x_n)\le\max\{x_1,\ldots,x_n,g\}+k$.

Note that no matter how many $g$ have parameter, when we use $\max$ function to express the inequality. Every value appears in the position of formal arguments $x_1,x_2,\ldots$ is a copy of some value in $x_1,\ldots,x_n$, or $0$. So can also express $g$ as
$$
\max\{x_1,\ldots,x_n,g\}+k\le\max\{k\cdot\max\{x_1,\ldots,x_n\}+l,x_1,\ldots,x_n\}+k=k\cdot\max\{x_1,\ldots,x_n\}+k+l
$$
Replace $l+k$ by $l$ due to the irrelevant relationship between $k$ and $l$. So we proved the argument.

(e) It is obvious $\mathscr{P}_1$ is a subset of primitive recursive function. To prove it is proper, consider $f(x)=x^2+l$, here we deliberately choose $l$ the same as the inequality in (d) since it is finite. We find that when $x>k$, the inequality will not hold anymore. This means $f$ is in $\mathscr{P}_1$. The argument is proved now.
