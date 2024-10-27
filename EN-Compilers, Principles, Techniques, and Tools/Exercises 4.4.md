# Exercises 4.4

## Problem 1

### Problem Description

For each of the following grammars, devise predictive parsers and show the parsing tables. You may left-factor and/or eliminate left-recursion from you grammars first.

a) The grammar of Exercise 4.2.2(a).

b) The grammar of Exercise 4.2.2(b).

c) The grammar of Exercise 4.2.2(c).

d) The grammar of Exercise 4.2.2(d).

e) The grammar of Exercise 4.2.2(e).

f) The grammar of Exercise 4.2.2(g).

### Solution

#### Question a

The grammar is
$$
S\rightarrow0S1\;|\;01
$$
$0$ is a left factor of $S$, then
$$
S\rightarrow 0A\\
A\rightarrow S1\;|\;1
$$
Now there’s no left factor.

For $S$
$$
S\rightarrow 0A\\
A\rightarrow 0A1\;|\;1
$$
Now left recursion is eliminated.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST     |
| ---- | --------- |
| $S$  | $\{0\}$   |
| $A$  | $\{0,1\}$ |

Since all productions begin with a terminal, the FIRST table is determined and FOLLOW table is useless.

##### Build Predictive Parsing Table

Consider all productions begin with terminal. Then

|      | $0$                | $1$              | \$   |
| ---- | ------------------ | ---------------- | ---- |
| $S$  | $S\rightarrow 0A$  |                  |      |
| $A$  | $A\rightarrow 0A1$ | $A\rightarrow 1$ |      |

Since all productions begin with a terminal, this is the answer.

#### Question b

The grammar is
$$
S\rightarrow +SS\;|\;*SS\;|\;a
$$
There’s no left factor as well as left recursion.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST       |
| ---- | ----------- |
| $S$  | $\{+,*,a\}$ |

Since all productions begin with a terminal, the FIRST table is determined and FOLLOW table is useless.

##### Build Predictive Parsing Table

Consider all productions begin with terminal. Then

|      | $+$                | $*$                | $a$              | \$   |
| ---- | ------------------ | ------------------ | ---------------- | ---- |
| $S$  | $S\rightarrow +SS$ | $S\rightarrow *SS$ | $S\rightarrow a$ |      |

Since all productions begin with a terminal, this is the answer.

#### Question c

The grammar is
$$
S\rightarrow S(S)S\;|\;\epsilon
$$
There’s no left factor but left recursive. First for $S$:
$$
S\rightarrow A\\
A\rightarrow (S)SA\;|\;\epsilon
$$
Now left recursion is eliminated.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST            |
| ---- | ---------------- |
| $S$  |                  |
| $A$  | $\{(,\epsilon\}$ |

###### $S\rightarrow A$

Elements in FIRST($A$) other than $\epsilon$ must be in FIRST($S$), as well as $\epsilon$. Which means $FIRST(S)=FIRST(S)\cup\{(,\epsilon\}$

|      | FIRST            |
| ---- | ---------------- |
| $S$  | $\{(,\epsilon\}$ |
| $A$  | $\{(,\epsilon\}$ |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW     |
| ---- | ---------- |
| $S$  | $\{),\$\}$ |
| $A$  |            |

###### $A\rightarrow(S)SA$

The second $S$ in production body means all the non-$\epsilon$ elements in FIRST($A$) must be in FOLLOW($S$), as well as FOLLOW($A$). Which means $\text{FOLLOW}(S)=\text{FOLLOW}(S)\{(,\text{FOLLOW}(A)\}$.

|      | FOLLOW                        |
| ---- | ----------------------------- |
| $S$  | $\{(,),\$,\text{FOLLOW}(A)\}$ |
| $A$  |                               |

###### $S\rightarrow A$

The $A$ in production body means FOLLOW($A$) contains FOLLOW($S$). Which means $\text{FOLLOW}(A)=\text{FOLLOW}(A)\cup\{\text{FOLLOW}(S)\}$

|      | FOLLOW                        |
| ---- | ----------------------------- |
| $S$  | $\{(,),\$,\text{FOLLOW}(A)\}$ |
| $A$  | $\{\text{FOLLOW}(S)\}$        |

###### Expand

Since FOLLOW($A$) and FOLLOW($S$) contains each other, they are equal. So

|      | FOLLOW       |
| ---- | ------------ |
| $S$  | $\{(,),\$\}$ |
| $A$  | $\{(,),\$\}$ |

##### Build Predictive Parsing Table

Consider all productions begin with terminal. Then

|      | (                   | )    | \$   |
| ---- | ------------------- | ---- | ---- |
| $S$  |                     |      |      |
| $A$  | $A\rightarrow(S)SA$ |      |      |

###### $A\rightarrow\epsilon$

We need to add it for any symbol in FOLLOW($A$):

|      | (                      | )                      | \$                     |
| ---- | ---------------------- | ---------------------- | ---------------------- |
| $S$  |                        |                        |                        |
| $A$  | $A\rightarrow(S)SA$    | $A\rightarrow\epsilon$ | $A\rightarrow\epsilon$ |
|      | $A\rightarrow\epsilon$ |                        |                        |

###### $S\rightarrow A$

We need to add it for any symbol in FIRST($A$) other than $\epsilon$, as well as FOLLOW($S$):

|      | (                      | )                      | \$                     |
| ---- | ---------------------- | ---------------------- | ---------------------- |
| $S$  | $S\rightarrow A$       | $S\rightarrow A$       | $S\rightarrow A$       |
| $A$  | $A\rightarrow(S)SA$    | $A\rightarrow\epsilon$ | $A\rightarrow\epsilon$ |
|      | $A\rightarrow\epsilon$ |                        |                        |

#### Question d

The grammar is
$$
S\rightarrow S+S\;|\;SS\;|\;(S)\;|\;S*\;|\;a
$$
$S$ is a left factor for $S$, so
$$
S\rightarrow SA\;|\;(S)\;|\;a\\
A\rightarrow +S\;|\;S\;|\;*
$$
Now there’s no left factor, but is left recursion. For $S$
$$
S\rightarrow (S)B\;|\;aB\\
B\rightarrow AB\;|\;\epsilon\\
A\rightarrow +S\;|\;S\;|\;*
$$
For $A$
$$
S\rightarrow (S)B\;|\;aB\\
B\rightarrow AB\;|\;\epsilon\\
A\rightarrow +S\;|\;(S)B\;|\;aB\;|\;*
$$

Now left recursion is eliminated.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST          |
| ---- | -------------- |
| $S$  | $\{(,a\}$      |
| $B$  | $\{\epsilon\}$ |
| $A$  | $\{+,(,a,*\}$  |

###### $B\rightarrow AB$

This means FIRST($B$) contains FIRST(A). Which means $\text{FIRST}(B)=\text{FIRST}(B)\cup\{+,(,a,*\}$

|      | FIRST                  |
| ---- | ---------------------- |
| $S$  | $\{(,a\}$              |
| $B$  | $\{+,(,a,*,\epsilon\}$ |
| $A$  | $\{+,(,a,*\}$          |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW     |
| ---- | ---------- |
| $S$  | $\{),\$\}$ |
| $B$  |            |
| $A$  |            |

###### $S\rightarrow(S)B\;|\;aB$

Both $B$ in production bodies mean FOLLOW($B$) contains FOLLOW($S$). Which mean $\text{FOLLOW}(B)=\text{FOLLOW}(B)\cup\{\text{FOLLOW}(S)\}$

|      | FOLLOW                 |
| ---- | ---------------------- |
| $S$  | $\{),\$\}$             |
| $B$  | $\{\text{FOLLOW}(S)\}$ |
| $A$  |                        |

###### $B\rightarrow AB$

The $A$ in production body means FOLLOW($A$) contains non-$\epsilon$ element in FIRST(B), as well as FOLLOW(B). Which means $\text{FOLLOW}(A)=\text{FOLLOW}(A)\cup\{+,(,a,*,\text{FOLLOW}(B)\}$

|      | FOLLOW                         |
| ---- | ------------------------------ |
| $S$  | $\{),\$\}$                     |
| $B$  | $\{\text{FOLLOW}(S)\}$         |
| $A$  | $\{+,(,a,*,\text{FOLLOW}(B)\}$ |

###### $A\rightarrow (S)B\;|\;aB$

Both $B$ in production bodies mean FOLLOW($B$) contain FOLLOW($A$). Which means $\text{FOLLOW}(B)=\text{FOLLOW}(B)\cup\{\text{FOLLOW}(A)\}$

|      | FOLLOW                                  |
| ---- | --------------------------------------- |
| $S$  | $\{),\$\}$                              |
| $B$  | $\{\text{FOLLOW}(S),\text{FOLLOW}(A)\}$ |
| $A$  | $\{+,(,a,*,\text{FOLLOW}(B)\}$          |

###### $A\rightarrow +S$

The $S$ in production body means FOLLOW($S$) contains FOLLOW($A$). Which means $\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{\text{FOLLOW}(A)\}$

|      | FOLLOW                                  |
| ---- | --------------------------------------- |
| $S$  | $\{),\$,\text{FOLLOW}(A)\}$             |
| $B$  | $\{\text{FOLLOW}(S),\text{FOLLOW}(A)\}$ |
| $A$  | $\{+,(,a,*,\text{FOLLOW}(B)\}$          |

###### Expand

Since FOLLOW($B$) contains FOLLOW($A$) and vice versa, then FOLLOW($A$) and FOLLOW($B$) are identical. Since FOLLOW($S$) contains FOLLOW($A$), and FOLLOW($B$) equals to FOLLOW($A$) contains FOLLOW($S$). FOLLOW($S$), FOLLOW($A$) and FOLLOW($B$) are identical. Then

|      | FOLLOW             |
| ---- | ------------------ |
| $S$  | $\{),\$,+,(,a,*\}$ |
| $B$  | $\{),\$,+,(,a,*\}$ |
| $A$  | $\{),\$,+,(,a,*\}$ |

##### Build Predictive Parsing Table

Consider all productions begin with terminal. Then

|      | (                  | )    | $+$               | $*$              | $a$               | \$   |
| ---- | ------------------ | ---- | ----------------- | ---------------- | ----------------- | ---- |
| $S$  | $S\rightarrow(S)B$ |      |                   |                  | $S\rightarrow aB$ |      |
| $B$  |                    |      |                   |                  |                   |      |
| $A$  | $A\rightarrow(S)B$ |      | $A\rightarrow +S$ | $A\rightarrow *$ | $A\rightarrow aB$ |      |

###### $B\rightarrow AB$

We need to add it for any symbol in FIRST($A$):

|      | (                  | )    | $+$               | $*$               | $a$               | \$   |
| ---- | ------------------ | ---- | ----------------- | ----------------- | ----------------- | ---- |
| $S$  | $S\rightarrow(S)B$ |      |                   |                   | $S\rightarrow aB$ |      |
| $B$  | $B\rightarrow AB$  |      | $B\rightarrow AB$ | $B\rightarrow AB$ | $B\rightarrow AB$ |      |
| $A$  | $A\rightarrow(S)B$ |      | $A\rightarrow +S$ | $A\rightarrow *$  | $A\rightarrow aB$ |      |

###### $B\rightarrow\epsilon$

We need to add it for any symbol in FOLLOW($B$):

|      | (                      | )                      | $+$                    | $*$                    | $a$                    | \$                     |
| ---- | ---------------------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- |
| $S$  | $S\rightarrow(S)B$     |                        |                        |                        | $S\rightarrow aB$      |                        |
| $B$  | $B\rightarrow AB$      | $B\rightarrow\epsilon$ | $B\rightarrow AB$      | $B\rightarrow AB$      | $B\rightarrow AB$      | $B\rightarrow\epsilon$ |
|      | $B\rightarrow\epsilon$ |                        | $B\rightarrow\epsilon$ | $B\rightarrow\epsilon$ | $B\rightarrow\epsilon$ |                        |
| $A$  | $A\rightarrow(S)B$     |                        | $A\rightarrow +S$      | $A\rightarrow *$       | $A\rightarrow aB$      |                        |

#### Question e

The grammar is
$$
S\rightarrow (L)\;|\;a\\
L\rightarrow L,S\;|\;S
$$
There’s no left factor but left recursion. For $L$
$$
S\rightarrow (L)\;|\;a\\
L\rightarrow SA\\
A\rightarrow ,SA\;|\;\epsilon
$$
For $L$
$$
S\rightarrow(L)\;|\;a\\
L\rightarrow(L)A\;|\;aA\\
A\rightarrow,SA\;|\;\epsilon
$$

Now left recursion is eliminated.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST            |
| ---- | ---------------- |
| $S$  | $\{(,a\}$        |
| $L$  | $\{(,a\}$        |
| $A$  | $\{,,\epsilon\}$ |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW   |
| ---- | -------- |
| $S$  | $\{\$\}$ |
| $L$  | $\{)\}$  |
| $A$  |          |

###### $L\rightarrow(L)A\;|\;aA$

The $A$ in both production bodies mean FOLLOW($A$) contains FOLLOW($L$). Which means $\text{FOLLOW}(A)=\text{FOLLOW}(A)\cup\{\text{FOLLOW}(L)\}$

|      | FOLLOW                 |
| ---- | ---------------------- |
| $S$  | $\{\$\}$               |
| $L$  | $\{)\}$                |
| $A$  | $\{\text{FOLLOW}(L)\}$ |

###### $A\rightarrow,SA$

The $S$ in production body means FOLLOW($S$) contains non-$\epsilon$ elements in FIRST($A$), as well as FOLLOW($A$). Which means $\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{,,\text{FOLLOW}(A)\}$

|      | FOLLOW                      |
| ---- | --------------------------- |
| $S$  | $\{\$,,,\text{FOLLOW}(A)\}$ |
| $L$  | $\{)\}$                     |
| $A$  | $\{\text{FOLLOW}(L)\}$      |

###### Expand

Directly calculate FOLLOW, then

|      | FOLLOW       |
| ---- | ------------ |
| $S$  | $\{\$,,,)\}$ |
| $L$  | $\{)\}$      |
| $A$  | $\{)\}$      |

##### Build Predictive Parsing Table

Consider all productions begin with terminal. Then

|      | (                  | )    | $a$               | ,                 | \$   |
| ---- | ------------------ | ---- | ----------------- | ----------------- | ---- |
| $S$  | $S\rightarrow(L)$  |      | $S\rightarrow a$  |                   |      |
| $L$  | $L\rightarrow(L)A$ |      | $S\rightarrow aA$ |                   |      |
| $A$  |                    |      |                   | $A\rightarrow,SA$ |      |

###### $A\rightarrow\epsilon$

We need to add it for any symbol in FOLLOW($A$)

|      | (                  | )                      | $a$               | ,                 | \$   |
| ---- | ------------------ | ---------------------- | ----------------- | ----------------- | ---- |
| $S$  | $S\rightarrow(L)$  |                        | $S\rightarrow a$  |                   |      |
| $L$  | $L\rightarrow(L)A$ |                        | $S\rightarrow aA$ |                   |      |
| $A$  |                    | $A\rightarrow\epsilon$ |                   | $A\rightarrow,SA$ |      |

#### Question f

The grammar is
$$
bexpr\rightarrow bexpr\textbf{ or }bterm\;|\;bterm\\
bterm\rightarrow bterm\textbf{ and } bfactor\;|\;bfactor\\
bfactor\rightarrow \textbf{not }bfactor\;|\;(bexpr)\;|\;\textbf{true}\;|\;\textbf{false}
$$
There is no left factor but left recursion. For $bexpr$
$$
bexpr\rightarrow bterm\;A\\
A\rightarrow \textbf{or }bterm\;A\;|\;\epsilon\\
bterm\rightarrow bterm\textbf{ and } bfactor\;|\;bfactor\\
bfactor\rightarrow \textbf{not }bfactor\;|\;(bexpr)\;|\;\textbf{true}\;|\;\textbf{false}
$$
For $bterm$
$$
bexpr\rightarrow bterm\;A\\
A\rightarrow \textbf{or }bterm\;A\;|\;\epsilon\\
bterm\rightarrow bfactor\;B\\
B\rightarrow\textbf{and }bfactor\;B\;|\;\epsilon\\
bfactor\rightarrow \textbf{not }bfactor\;|\;(bexpr)\;|\;\textbf{true}\;|\;\textbf{false}
$$

Now left recursion have been eliminated.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|           | FIRST                                             |
| --------- | ------------------------------------------------- |
| $bexpr$   |                                                   |
| $A$       | $\{\textbf{or},\epsilon\}$                        |
| $bterm$   |                                                   |
| $B$       | $\{\textbf{and},\epsilon\}$                       |
| $bfactor$ | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |

###### $bterm\rightarrow bfactor\;B$

This means FIRST($bterm$) contains FIRST($bfactor$). Which means $\text{FIRST}(bterm)=\text{FIRST}(bterm)\cup\{\textbf{not},(,\textbf{true},\textbf{false}\}$

|           | FIRST                                             |
| --------- | ------------------------------------------------- |
| $bexpr$   |                                                   |
| $A$       | $\{\textbf{or},\epsilon\}$                        |
| $bterm$   | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |
| $B$       | $\{\textbf{and},\epsilon\}$                       |
| $bfactor$ | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |

###### $bexpr\rightarrow bterm\;A$

This means FIRST($bexpr$) contains FIRST($bterm$). Which means $\text{FIRST}(bexpr)=\text{FIRST}(bexpr)\cup\{\textbf{not},(,\textbf{true},\textbf{false}\}$

|           | FIRST                                             |
| --------- | ------------------------------------------------- |
| $bexpr$   | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |
| $A$       | $\{\textbf{or},\epsilon\}$                        |
| $bterm$   | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |
| $B$       | $\{\textbf{and},\epsilon\}$                       |
| $bfactor$ | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($bexpr$):

|           | FOLLOW     |
| --------- | ---------- |
| $bexpr$   | $\{),\$\}$ |
| $A$       |            |
| $bterm$   |            |
| $B$       |            |
| $bfactor$ |            |

###### $B\rightarrow\textbf{and }bfactor\;B$

$bfactor$ in production body means FOLLOW($bfactor$) contains non-$\epsilon$ elements in FIRST($B$), as well as FOLLOW($B$). Which means $\text{FOLLOW}(bfactor)=\text{FOLLOW}(bfactor)\cup\{\textbf{and},\text{FOLLOW}(B)\}$

|           | FOLLOW                              |
| --------- | ----------------------------------- |
| $bexpr$   | $\{),\$\}$                          |
| $A$       |                                     |
| $bterm$   |                                     |
| $B$       |                                     |
| $bfactor$ | $\{\textbf{and},\text{FOLLOW}(B)\}$ |

###### $bterm\rightarrow bfactor\;B$

$bfactor$ in production body means FOLLOW($bfactor$) contains non-$\epsilon$ elements in FIRST($B$), as well as FOLLOW($bterm$). Which means $\text{FOLLOW}(bfactor)=\text{FOLLOW}(bfactor)\cup\{\textbf{and},\text{FOLLOW}(bterm)\}$.

$B$ in production body means FOLLOW($B$) contains FOLLOW($bterm$). Which means $\text{FOLLOW}(B)=\text{FOLLOW}(B)\cup\{\text{FOLLOW}(bterm)\}$

|           | FOLLOW                                                   |
| --------- | -------------------------------------------------------- |
| $bexpr$   | $\{),\$\}$                                               |
| $A$       |                                                          |
| $bterm$   |                                                          |
| $B$       | $\{\text{FOLLOW}(bterm)\}$                               |
| $bfactor$ | $\{\textbf{and},\text{FOLLOW}(B),\text{FOLLOW}(bterm)\}$ |

###### $A\rightarrow \textbf{or }bterm\;A$

$bterm$ in production body means FOLLOW($bterm$) contains non-$\epsilon$ elements in FIRST($A$), as well as FOLLOW($A$). Which means $\text{FOLLOW}(bterm)=\text{FOLLOW}(bterm)\cup\{\textbf{or},\text{FOLLOW}(A)\}$

|           | FOLLOW                                                   |
| --------- | -------------------------------------------------------- |
| $bexpr$   | $\{),\$\}$                                               |
| $A$       |                                                          |
| $bterm$   | $\{\textbf{or},\text{FOLLOW}(A)\}$                       |
| $B$       | $\{\text{FOLLOW}(bterm)\}$                               |
| $bfactor$ | $\{\textbf{and},\text{FOLLOW}(B),\text{FOLLOW}(bterm)\}$ |

###### $bexpr\rightarrow bterm\;A$

$bterm$ in production body means FOLLOW($bterm$) contains non-$\epsilon$ elements in FIRST($A$), as well as FOLLOW($bexpr$). Which means $\text{FOLLOW}(bterm)=\text{FOLLOW}(bterm)\cup\{\textbf{or},\text{FOLLOW}(bexpr)\}$

|           | FOLLOW                                                   |
| --------- | -------------------------------------------------------- |
| $bexpr$   | $\{),\$\}$                                               |
| $A$       | $\{\text{FOLLOW}(bexpr)\}$                               |
| $bterm$   | $\{\textbf{or},\text{FOLLOW}(A),\text{FOLLOW}(bexpr)\}$  |
| $B$       | $\{\text{FOLLOW}(bterm)\}$                               |
| $bfactor$ | $\{\textbf{and},\text{FOLLOW}(B),\text{FOLLOW}(bterm)\}$ |

###### Expand

Directly calculate FOLLOW, then

|           | FOLLOW                              |
| --------- | ----------------------------------- |
| $bexpr$   | $\{),\$\}$                          |
| $A$       | $\{),\$\}$                          |
| $bterm$   | $\{\textbf{or},),\$\}$              |
| $B$       | $\{\textbf{or},),\$\}$              |
| $bfactor$ | $\{\textbf{and},\textbf{or},),\$\}$ |

##### Build Predictive Parsing Table

Consider all productions begin with terminal. Then

|           | and                                   | or                                 | not                                       | (                           | )    | true                              | false                              | \$   |
| --------- | ------------------------------------- | ---------------------------------- | ----------------------------------------- | --------------------------- | ---- | --------------------------------- | ---------------------------------- | ---- |
| $bexpr$   |                                       |                                    |                                           |                             |      |                                   |                                    |      |
| $A$       |                                       | $A\rightarrow\textbf{or }bterm\;A$ |                                           |                             |      |                                   |                                    |      |
| $bterm$   |                                       |                                    |                                           |                             |      |                                   |                                    |      |
| $B$       | $B\rightarrow\textbf{and }bfactor\;B$ |                                    |                                           |                             |      |                                   |                                    |      |
| $bfactor$ |                                       |                                    | $bfactor\rightarrow \textbf{not }bfactor$ | $bfactor\rightarrow(bexpr)$ |      | $bfactor\rightarrow\textbf{true}$ | $bfactor\rightarrow\textbf{false}$ |      |

###### $B\rightarrow\epsilon$

We need to add it to any symbol in FOLLOW($B$):

|           | and                                   | or                                 | not                                       | (                           | )                      | true                              | false                              | \$                     |
| --------- | ------------------------------------- | ---------------------------------- | ----------------------------------------- | --------------------------- | ---------------------- | --------------------------------- | ---------------------------------- | ---------------------- |
| $bexpr$   |                                       |                                    |                                           |                             |                        |                                   |                                    |                        |
| $A$       |                                       | $A\rightarrow\textbf{or }bterm\;A$ |                                           |                             |                        |                                   |                                    |                        |
| $bterm$   |                                       |                                    |                                           |                             |                        |                                   |                                    |                        |
| $B$       | $B\rightarrow\textbf{and }bfactor\;B$ | $B\rightarrow\epsilon$             |                                           |                             | $B\rightarrow\epsilon$ |                                   |                                    | $B\rightarrow\epsilon$ |
| $bfactor$ |                                       |                                    | $bfactor\rightarrow \textbf{not }bfactor$ | $bfactor\rightarrow(bexpr)$ |                        | $bfactor\rightarrow\textbf{true}$ | $bfactor\rightarrow\textbf{false}$ |                        |

###### $bterm\rightarrow bfactor\;B$

We need to add it to any symbol in FIRST($bfactor$):

|           | and                                   | or                                 | not                                       | (                             | )                      | true                              | false                              | \$                     |
| --------- | ------------------------------------- | ---------------------------------- | ----------------------------------------- | ----------------------------- | ---------------------- | --------------------------------- | ---------------------------------- | ---------------------- |
| $bexpr$   |                                       |                                    |                                           |                               |                        |                                   |                                    |                        |
| $A$       |                                       | $A\rightarrow\textbf{or }bterm\;A$ |                                           |                               |                        |                                   |                                    |                        |
| $bterm$   |                                       |                                    | $bterm\rightarrow bfactor\;B$             | $bterm\rightarrow bfactor\;B$ |                        | $bterm\rightarrow bfactor\;B$     | $bterm\rightarrow bfactor\;B$      |                        |
| $B$       | $B\rightarrow\textbf{and }bfactor\;B$ | $B\rightarrow\epsilon$             |                                           |                               | $B\rightarrow\epsilon$ |                                   |                                    | $B\rightarrow\epsilon$ |
| $bfactor$ |                                       |                                    | $bfactor\rightarrow \textbf{not }bfactor$ | $bfactor\rightarrow(bexpr)$   |                        | $bfactor\rightarrow\textbf{true}$ | $bfactor\rightarrow\textbf{false}$ |                        |

###### $A\rightarrow\epsilon$

We need to add it to any symbol in FOLLOW($A$):

|           | and                                   | or                                 | not                                       | (                             | )                      | true                              | false                              | \$                     |
| --------- | ------------------------------------- | ---------------------------------- | ----------------------------------------- | ----------------------------- | ---------------------- | --------------------------------- | ---------------------------------- | ---------------------- |
| $bexpr$   |                                       |                                    |                                           |                               |                        |                                   |                                    |                        |
| $A$       |                                       | $A\rightarrow\textbf{or }bterm\;A$ |                                           |                               | $A\rightarrow\epsilon$ |                                   |                                    | $A\rightarrow\epsilon$ |
| $bterm$   |                                       |                                    | $bterm\rightarrow bfactor\;B$             | $bterm\rightarrow bfactor\;B$ |                        | $bterm\rightarrow bfactor\;B$     | $bterm\rightarrow bfactor\;B$      |                        |
| $B$       | $B\rightarrow\textbf{and }bfactor\;B$ | $B\rightarrow\epsilon$             |                                           |                               | $B\rightarrow\epsilon$ |                                   |                                    | $B\rightarrow\epsilon$ |
| $bfactor$ |                                       |                                    | $bfactor\rightarrow \textbf{not }bfactor$ | $bfactor\rightarrow(bexpr)$   |                        | $bfactor\rightarrow\textbf{true}$ | $bfactor\rightarrow\textbf{false}$ |                        |

###### $bexpr\rightarrow bterm\;A$

We need to add it to any symbol in FIRST($bterm$):

|           | and                                   | or                                 | not                                       | (                             | )                      | true                              | false                              | \$                     |
| --------- | ------------------------------------- | ---------------------------------- | ----------------------------------------- | ----------------------------- | ---------------------- | --------------------------------- | ---------------------------------- | ---------------------- |
| $bexpr$   |                                       |                                    | $bexpr\rightarrow bterm\;A$               | $bexpr\rightarrow bterm\;A$   |                        | $bexpr\rightarrow bterm\;A$       | $bexpr\rightarrow bterm\;A$        |                        |
| $A$       |                                       | $A\rightarrow\textbf{or }bterm\;A$ |                                           |                               | $A\rightarrow\epsilon$ |                                   |                                    | $A\rightarrow\epsilon$ |
| $bterm$   |                                       |                                    | $bterm\rightarrow bfactor\;B$             | $bterm\rightarrow bfactor\;B$ |                        | $bterm\rightarrow bfactor\;B$     | $bterm\rightarrow bfactor\;B$      |                        |
| $B$       | $B\rightarrow\textbf{and }bfactor\;B$ | $B\rightarrow\epsilon$             |                                           |                               | $B\rightarrow\epsilon$ |                                   |                                    | $B\rightarrow\epsilon$ |
| $bfactor$ |                                       |                                    | $bfactor\rightarrow \textbf{not }bfactor$ | $bfactor\rightarrow(bexpr)$   |                        | $bfactor\rightarrow\textbf{true}$ | $bfactor\rightarrow\textbf{false}$ |                        |

## Problem 2

### Problem Description

Is it possible, by modifying the grammar in any way, to construct a predictive parser for the language of Exercise 4.2.1 (postfix expressions with operand $a$).

### Solution

The grammar is
$$
S\rightarrow SS+\;|\;SS*\;|\;a
$$
Since $SS$ is left factor, then
$$
S\rightarrow SSA\;|\;a\\
A\rightarrow+\;|\;*
$$
Now there’s no left factro but left recursion. For $S$
$$
S\rightarrow aB\\
B\rightarrow SAB\;|\;\epsilon\\
A\rightarrow+\;|\;*
$$
For $B$
$$
S\rightarrow aB\\
B\rightarrow aBAB\;|\;\epsilon\\
A\rightarrow+\;|\;*
$$
Now the left recursion is eliminated.

#### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST            |
| ---- | ---------------- |
| $S$  | $\{a\}$          |
| $B$  | $\{a,\epsilon\}$ |
| $A$  | $\{+,*\}$        |

#### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FIRST    |
| ---- | -------- |
| $S$  | $\{\$\}$ |
| $B$  |          |
| $A$  |          |

##### $S\rightarrow aB$

The $B$ in production body means FOLLOW($B$) contains FOLLOW($S$). Which means $\text{FOLLOW}(B)=\text{FOLLOW}(B)\cup\{\text{FOLLOW}(S)\}$:

|      | FIRST                  |
| ---- | ---------------------- |
| $S$  | $\{\$\}$               |
| $B$  | $\{\text{FOLLOW}(S)\}$ |
| $A$  |                        |

##### $B\rightarrow aBAB$

The first $B$ in production means FOLLOW($B$) contains FIRST($A$). Which means $\text{FOLLOW}(B)=\text{FOLLOW}(B)\cup\{+,*\}$.

The first $A$ in production means FOLLOW($A$) contains non-$\epsilon$ elements in $B$, as well as FOLLOW($B$). Which means $\text{FOLLOW}(A)=\text{FOLLOW}(A)\cup\{a,\text{FOLLOW}(B)\}$. Then

|      | FOLLOW                     |
| ---- | -------------------------- |
| $S$  | $\{\$\}$                   |
| $B$  | $\{\text{FOLLOW}(S),+,*\}$ |
| $A$  | $\{a,\text{FOLLOW}(B)\}$   |

##### Expand

Directly calculate FOLLOW, then

|      | FOLLOW         |
| ---- | -------------- |
| $S$  | $\{\$\}$       |
| $B$  | $\{\$,+,*\}$   |
| $A$  | $\{a,\$,+,*\}$ |

#### Build Parsing Table

Consider all productions begin with terminal. Then

|      | $a$                 | $+$              | $*$             | \$   |
| ---- | ------------------- | ---------------- | --------------- | ---- |
| $S$  | $S\rightarrow aB$   |                  |                 |      |
| $B$  | $B\rightarrow aBAB$ |                  |                 |      |
| $A$  |                     | $A\rightarrow +$ | $A\rightarrow*$ |      |

##### $B\rightarrow\epsilon$

We need to add it to any symbol in FOLLOW($B$):

|      | $a$                 | $+$                    | $*$                    | \$                     |
| ---- | ------------------- | ---------------------- | ---------------------- | ---------------------- |
| $S$  | $S\rightarrow aB$   |                        |                        |                        |
| $B$  | $B\rightarrow aBAB$ | $B\rightarrow\epsilon$ | $B\rightarrow\epsilon$ | $B\rightarrow\epsilon$ |
| $A$  |                     | $A\rightarrow +$       | $A\rightarrow*$        |                        |

Since the parsing table have unique value for each entry, this grammar is a LL(1) grammar.

## Problem 3

### Problem Description

Compute FIRST and FOLLOW for the grammar of Exercise 4.2.1.

### Solution

The grammar is
$$
S\rightarrow SS+\;|\;SS*\;|\;a
$$
#### $S$ does not contain $\epsilon$

$\epsilon$ is of length $0$. However, every derivation of $S$ will introduce one token and every sentence must be derived at least once. Then $S$ does not contain $\epsilon$.

#### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST   |
| ---- | ------- |
| $S$  | $\{a\}$ |

##### $S\rightarrow SS+\;|\;SS*$

Since $S$ can’t be $\epsilon$, these productions won’t affect FIRST table.

#### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW       |
| ---- | ------------ |
| $S$  | $\{+,*,\$\}$ |

##### $S\rightarrow SS+$

Since $S$ can’t be $\epsilon$, the first $S$ means FOLLOW($S$) contains FIRST($S$). Which means $\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{a\}$.

|      | FOLLOW         |
| ---- | -------------- |
| $S$  | $\{a,+,*,\$\}$ |

##### $S\rightarrow SS*$

Since $S$ can’t be $\epsilon$, the first $S$ means FOLLOW($S$) contains FIRST($S$). Which means $\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{a\}$.

|      | FOLLOW         |
| ---- | -------------- |
| $S$  | $\{a,+,*,\$\}$ |

## Problem 4

### Problem Description

Compute FIRST and FOLLOW for each of the grammars of Exercise 4.2.2.

### Solution

#### a)

The grammar is
$$
S\rightarrow 0S1\;|\;01
$$

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST   |
| ---- | ------- |
| $S$  | $\{0\}$ |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW     |
| ---- | ---------- |
| $S$  | $\{1,\$\}$ |

#### b)

The grammar is
$$
S\rightarrow +SS\;|\;*SS\;|\;a
$$

##### $S$ does not contain $\epsilon$

$\epsilon$ is of length $0$. However, every derivation of $S$ will introduce one token and every sentence must be derived at least once. Then $S$ does not contain $\epsilon$.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST       |
| ---- | ----------- |
| $S$  | $\{+,*,a\}$ |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW   |
| ---- | -------- |
| $S$  | $\{\$\}$ |

###### $S\rightarrow +SS$

Since $S$ can’t be $\epsilon$, the first $S$ means FOLLOW($S$) contains FIRST($S$). Which means $\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{+,*,a\}$

|      | FOLLOW         |
| ---- | -------------- |
| $S$  | $\{+,*,a,\$\}$ |

###### $S\rightarrow *SS$

Since $S$ can’t be $\epsilon$, the first $S$ means FOLLOW($S$) contains FIRST($S$). Which means $\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{+,*,a\}$

|      | FOLLOW         |
| ---- | -------------- |
| $S$  | $\{+,*,a,\$\}$ |

#### c)

The grammar is
$$
S\rightarrow S(S)S\;|\;\epsilon
$$

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST          |
| ---- | -------------- |
| $S$  | $\{\epsilon\}$ |

###### $S\rightarrow S(S)S$

Since $S$ can be $\epsilon$, the FIRST($S$) contains (.

|      | FIRST            |
| ---- | ---------------- |
| $S$  | $\{(,\epsilon\}$ |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW       |
| ---- | ------------ |
| $S$  | $\{(,),\$\}$ |

#### d)

The grammar is
$$
S\rightarrow S+S\;|\;SS\;|\;(S)\;|\;S*\;|\;a
$$


##### $S$ does not contain $\epsilon$

$\epsilon$ is of length $0$. Productions except $S\rightarrow SS$ will introduce one terminal, $S$ can never derivate a sentence without using productions other than $S\rightarrow SS$ at least once. Then $S$ does not contain $\epsilon$.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST     |
| ---- | --------- |
| $S$  | $\{(,a\}$ |

###### $S\rightarrow S+S\;|\;SS\;|\;S*$

Since $S$ can’t be $\epsilon$, these productions won’t affect FIRST table.

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW         |
| ---- | -------------- |
| $S$  | $\{+,),*,\$\}$ |

###### $S\rightarrow SS$

Since $S$ can’t be $\epsilon$. The first $S$ in production body means FOLLOW($S$) contains FIRST($S$). Which means $\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{(,a\}$

|      | FOLLOW             |
| ---- | ------------------ |
| $S$  | $\{(,),+,*,a,\$\}$ |

#### e)

The grammar is
$$
S\rightarrow (L)\;|\;a\\
L\rightarrow L,S\;|\;S
$$

##### $L$ does not contain $\epsilon$

$\epsilon$ is of length $0$. However, every derivation of $S$ will introduce at least one token and every sentence must be derived at least once. Then $S$ does not contain $\epsilon$, and every derivation of $L$ will introduce a $S$, which does not contain $\epsilon$ and every sentence must be derived at least once. Then $L$ does not contain $\epsilon$.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST     |
| ---- | --------- |
| $S$  | $\{(,a\}$ |
| $L$  |           |

###### $L\rightarrow S$

Since $S$ can’t be $\epsilon$, then FIRST($L$) contains FIRST($S$). Which means $\text{FIRST}(L)=\text{FIRST}(L)\cup\{(,a\}$

|      | FIRST     |
| ---- | --------- |
| $S$  | $\{(,a\}$ |
| $L$  | $\{(,a\}$ |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW    |
| ---- | --------- |
| $S$  | $\{\$\}$  |
| $L$  | $\{,,)\}$ |

###### $L\rightarrow L,S\;|\;S$

The $S$ in both production bodies mean FOLLOW($S$) contains FOLLOW($L$). Which means $\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{\text{FOLLOW}(L)\}$

|      | FOLLOW                    |
| ---- | ------------------------- |
| $S$  | $\{\$,\text{FOLLOW}(L)\}$ |
| $L$  | $\{,,)\}$                 |

###### Expand

Directly calculate FOLLOW, then

|      | FOLLOW       |
| ---- | ------------ |
| $S$  | $\{\$,,,)\}$ |
| $L$  | $\{,,)\}$    |

#### f)

The grammar is
$$
S\rightarrow aSbS\;|\;bSaS\;|\;\epsilon
$$

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|      | FIRST              |
| ---- | ------------------ |
| $S$  | $\{a,b,\epsilon\}$ |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($S$):

|      | FOLLOW       |
| ---- | ------------ |
| $S$  | $\{a,b,\$\}$ |

#### g)

The grammar is
$$
bexpr\rightarrow bexpr\textbf{ or }bterm\;|\;bterm\\
bterm\rightarrow bterm\textbf{ and } bfactor\;|\;bfactor\\
bfactor\rightarrow \textbf{not }bfactor\;|\;(bexpr)\;|\;\textbf{true}\;|\;\textbf{false}
$$

##### $bexpr$ does not contain $\epsilon$

$\epsilon$ is of length $0$. However, every derivation of $bfactor$ will introduce at least one token and every sentence must be derived at least once. Then $bfactor$ does not contain $\epsilon$, and every derivation of $bterm$ will introduce a $bfactor$, which does not contain $\epsilon$ and every sentence must be derived at least once. Then $bterm$ does not contain $\epsilon$. The same for $bexpr$.

##### FIRST Calculation

Consider all productions begin with terminal or is $\epsilon$. Then

|           | FIRST                                             |
| --------- | ------------------------------------------------- |
| $bexpr$   |                                                   |
| $bterm$   |                                                   |
| $bfactor$ | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |

###### $bterm\rightarrow bfactor$

This means FIRST($bterm$) contains FIRST($bfactor$). Which means $\text{FIRST}(bterm)=\text{FIRST}(bterm)\cup\{\textbf{not},(,\textbf{true},\textbf{false}\}$

|           | FIRST                                             |
| --------- | ------------------------------------------------- |
| $bexpr$   |                                                   |
| $bterm$   | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |
| $bfactor$ | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |

###### $bexpr\rightarrow bterm$

This means FIRST($bexpr$) contains FIRST($bterm$). Which means $\text{FIRST}(bexpr)=\text{FIRST}(bexpr)\cup\{\textbf{not},(,\textbf{true},\textbf{false}\}$

|           | FIRST                                             |
| --------- | ------------------------------------------------- |
| $bexpr$   | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |
| $bterm$   | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |
| $bfactor$ | $\{\textbf{not},(,\textbf{true},\textbf{false}\}$ |

##### FOLLOW Calculation

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($bexpr$):

|           | FOLLOW                 |
| --------- | ---------------------- |
| $bexpr$   | $\{\textbf{or},),\$\}$ |
| $bterm$   | $\{\textbf{and}\}$     |
| $bfactor$ |                        |

###### $bexpr\rightarrow bexpr\textbf{ or }bterm\;|\;bterm$

The $bterm$ in both production bodies mean FOLLOW($bterm$) contains FOLLOW($bexpr$). Which means $\text{FOLLOW}(bterm)=\text{FOLLOW}(bterm)\cup\{\text{FOLLOW}(bexpr)\}$

|           | FOLLOW                                  |
| --------- | --------------------------------------- |
| $bexpr$   | $\{\textbf{or},),\$\}$                  |
| $bterm$   | $\{\textbf{and},\text{FOLLOW}(bexpr)\}$ |
| $bfactor$ |                                         |

###### $bterm\rightarrow bterm\textbf{ and } bfactor\;|\;bfactor$

The $bfactor$ in both production bodies mean FOLLOW($bfactor$) contains FOLLOW($bterm$). Which means $\text{FOLLOW}(bfactor)=\text{FOLLOW}(bfactor)\cup\{\text{FOLLOW}(bterm)\}$

|           | FOLLOW                                  |
| --------- | --------------------------------------- |
| $bexpr$   | $\{\textbf{or},),\$\}$                  |
| $bterm$   | $\{\textbf{and},\text{FOLLOW}(bexpr)\}$ |
| $bfactor$ | $\{\text{FOLLOW}(bterm)\}$              |

###### Expand

Directly calculate FOLLOW, then

|           | FOLLOW                              |
| --------- | ----------------------------------- |
| $bexpr$   | $\{\textbf{or},),\$\}$              |
| $bterm$   | $\{\textbf{and},\textbf{or},),\$\}$ |
| $bfactor$ | $\{\textbf{and},\textbf{or},),\$\}$ |

## Problem 5

### Problem Description

The grammar $S\rightarrow aSa\;|\;aa$ generates all even-length strings of $a$’s. We can devise a recursive-descent parser with backtrack for this grammar. If we choose to expand by production $S\rightarrow aa$ first, then we shall only recognize the string $aa$. Thus, any reasonable recursive-descent parser will try $S\rightarrow aSa$ first.

a) Show that this recursive-descent parser recognizes inputs $aa$, $aaaa$, and $aaaaaaaa$ but not $aaaaaa$.

b) What language does this recursive-descent parser recognize?

### Solution

Since the grammar will generate all even-length strings of $a$’s, the parser will recognize a subset of it. Let recursion layer $l$ denotes how many times $S$ is derived.

First, $S\Rightarrow aSa$ will keep going on until $l=n+1$. Let $k$ denotes the current reading position of input, now $k=n+1$ holds and both derivations will fail. So it must go to state $k=n+1,l=n$. If the initial derivation $S\Rightarrow aSa$ is true, that means the end state is $i=n,l=2$. The only possible counterpart is the input $aa$, where the $S\Rightarrow aSa$ must fail.

Assume a function have a state $k=k_0,l=l_0$, then the outer function will be such a state when it ends: if $k_0=n+1$, $i=l_0+1$. Otherwise $i=k_0+1$. And then $l=l_0-1$. For $aa$, it starts with $i=3,l=2$. This would deny $S\Rightarrow aSa$ and choose $S\Rightarrow aa$ and scan from first character for both strings. And $aa$ is in language.

For other strings, the start state can go further to $i=n,l=n-2$, this means $n=4$ is in the language. Further $(i,l)=(n,n-2)\rightarrow(n+1,n-3)\rightarrow(n-2,n-4)$ shows that $n=6$ is not in the language. Then $(n-2,n-4)\rightarrow(n,n-6)$ shows $n=8$ is in the language.

Prove $n=2^k(k>1)$ by induction. $k=2$ has been proven. $(n,n-2^k+2)\rightarrow(n-2^k+2,n-2^k)\rightarrow(n,n-2^{k+1}+2)$ finishes the induction. Combined with $n=2$ is in the language. All string of $a$’s with length of $2^k(k\ge 1)$ will in this language.

## Problem 6

### Problem Description

A grammar is $\epsilon$-*free* is no production body is $\epsilon$ (called an $\epsilon$-*production*).

a) Give an algorithm to convert any grammar into an $\epsilon$-free grammar that generates the same language (with the possible exception of the empty string — no $\epsilon$-free grammar can generate $\epsilon$).

b) Apply your algorithm to the grammar $S\rightarrow aSbS\;|\;bSaS\;|\;\epsilon$. *Hint*: First find all the nonterminals that are *nullable*, meaning that they generate $\epsilon$, perhaps by a long derivation.

### Solution

#### a)

1. Let $\Pi_0$ contains all nonterminals with $\epsilon$-production.
2. Replace nonterminals in $\Pi_0$ with $\epsilon$ for each production. And let $\Pi$ contains all nonterminals with $\epsilon$-productions now.
3. If $\Pi$ equals to $\Pi_0$, continue. Otherwise, assign $\Pi$ to $\Pi_0$, and go back to step 2.
4. For each production and for each nonterminal $N_i$ in $\Pi_0$ appears in the production, exhausting all possible values of these nonterminals between $\epsilon$ and $N_i$.
5. For nonterminals other than start symbol $S$, discard $\epsilon$-productions. If $S$ has $\epsilon$-production, replace it with $S'\rightarrow\epsilon\;|\;S$.

#### b)

For step 1, $\Pi_0=\{S\}$. And since there’s only one nonterminal, step 2 and step 3 won’t change $\Pi_0$.

For step 4, we can get
$$
S\rightarrow ab\;|\;aSb\;|\;abS\;|\;aSbS\;|\;ba\;|\;bSa\;|\;baS\;|\;bSaS\;|\;\epsilon
$$
For step 5, we can get
$$
S'\rightarrow \epsilon\;|\;S\\
S\rightarrow ab\;|\;aSb\;|\;abS\;|\;aSbS\;|\;ba\;|\;bSa\;|\;baS\;|\;bSaS
$$

## Problem 7

### Problem Description

A *single production* is a production whose body is a single nonterminal, i.e., a production of the form $A\rightarrow A$.

a) Give an algorithm to convert any grammar into an $\epsilon$-free grammar, with no single productions, that generates the same language (with the possible exception of the empty string) *Hint*: First eliminate $\epsilon$-productions, and then find for which pairs of nonterminals $A$ and $B$ does $A\overset{*}{\Rightarrow}B$ by a sequence of single productions.

b) Apply your algorithm to the grammar (4.1) in Section 4.1.2.

c) Show that, as a consequence of part (a), we can convert a grammar into an equivalent grammar that has no *cycle* (derivations of one or more steps in which $A\overset{*}{\Rightarrow}A$ for some nonterminal $A$).

### Solution

#### a)

1. Eliminate $\epsilon$-productions and redundant single production.
2. Let $\Pi$ be the set of nonterminal which has no single production. Expand any single production with nonterminal in $\Pi$ as its body.
3. Recalculate $\Pi$, if $\Pi$ does not contain every nonterminal other than $S'$, repeat step 2. Otherwise terminate.

#### b)

The grammar is
$$
E\rightarrow E+T\;|\;T\\
T\rightarrow T*F\;|\;F\\
F\rightarrow (E)\;|\;\textbf{id}
$$
For step 1, there’s no $\epsilon$-productions and redundant single production.

$\Pi=\{F\}$, and replace $F$ in single productions:
$$
E\rightarrow E+T\;|\;T\\
T\rightarrow T*F\;|\;(E)\;|\;\textbf{id}\\
F\rightarrow (E)\;|\;\textbf{id}
$$
$\Pi=\{T,F\}$, and replace $T$ in single productions:
$$
E\rightarrow E+T\;|\;T*F\;|\;(E)\;|\;\textbf{id}\\
T\rightarrow T*F\;|\;(E)\;|\;\textbf{id}\\
F\rightarrow (E)\;|\;\textbf{id}
$$

#### c)

First of all, due to how $S'$ is generated, there’s no possibility for $S'\overset{*}{\Rightarrow}S'$. For other nonterminals, prove by induction on derive times $m$.

When $m=1$, if any nonterminal $A\Rightarrow A$, however this production is eliminated in step 1.

When $m=k+1$, consider about the first $k$ derivation of $A$, $A\overset{k}{\Rightarrow}\alpha X\beta$, where nonterminal $X$ can be identical to $A$. If $X$ is not identical to $A$, there must be $\alpha X\beta\Rightarrow \alpha\alpha_1A\beta_1\beta$, $\alpha_1$ and $\beta_1$ can’t both be $\epsilon$ so $\alpha\alpha_1,\beta\beta_1$ can’t both be $\epsilon$ either. If $X$ is identical to $A$, then $\alpha,\beta$ can’t both be $\epsilon$, from the similar statement, the induction is proved.

##  Problem 8

### Problem Description

A grammar is said to be in *Chomsky Normal Form* (CNF) is every production is either of the form $A\rightarrow BC$ or of the form $A\rightarrow a$, where $A$, $B$, and $C$ are nonterminals, and $a$ is a terminal. Show how to convert any grammar into a CNF grammar for the same language (with the possible exception of the empty string — no CNF grammar can generate $\epsilon$).

### Solution

1. Eliminate $\epsilon$-productions and cycles.
2. If some production has a body of length 2, replace occurrences of $a$ with a nonterminal $X$ and add production $X\rightarrow a$.
3. If some production has a body of length more than $2$, such as $A\rightarrow X\alpha$. Deal with the $X$ similarly as step 2, and add production $Y\rightarrow\alpha$.
4. If there still exists production is not of the two form, go back to 2. Otherwise, terminate.

## Problem 9

### Problem Description

Every language that has a context-free grammar can be recognized in at most $O(n^3)$ time for strings of lenth $n$. A simple way to do so, called the *Cocke-Younger-Kasami* (or CYK) algorithm is based on dynamic programming. That is, given a string $a_1a_2\cdots a_n$, we construct an $n$-by-$n$ table $T$ such that $T_{ij}$ is the set of nonterminals that generate the substring $a_ia_{i+1}\cdots a_j$. If the underlying grammar is in CNF (see Exercise 4.4.8), then one table entry can be filled in in $O(n)$ time, provided we fill the entries in the proper order: lowest value of $j-i$ first. Write an algorithm that correctly fills in the entries of the table, and show that your algorithm takes $O(n^3)$ time. Having filled in the table, how do you determine whether $a_1a_2\cdots a_n$ is in the language.

### Solution

1. Fill $T_{ij}$ where $i=j$ with nonterminal that owns production such as $A\rightarrow a_i$.
2. Fill $T_{ij}$ for $j-i=n$ with nonterminal $A$ that owns production such as $A\rightarrow T_{ik}T_{(k+1)j}$ for any $i\le k<j$.
3. Repeat the above dynamic programming procedure until all $T_{ij}$ is calculated.

Every check of the existence of grammar takes $O(1)$ time, and every entry will try $O(n)$ possibilities. Since there’s $O(n^2)$ entries. It will cost $O(n^3)$ to fill the table.

By checking whether the start symbol is in $T_{1n}$, we can determine whether $a_1a_2\cdots a_n$ is in the language.

## Problem 10

### Problem Description

Show how, having filled in the table as in Exercise 4.4.9, we can in $O(n)$ time recorver a parse tree for $a_1a_2\cdots a_n$. *Hint*: modify the table so it records, for each nonterminal $A$ in each table entry $T_{ij}$, some pair of nonterminals in other table entries that justified putting $A$ in $T_{ij}$.

### Solution

For the first time a new nonterminal $A$ is put into $T_{ij}$, record which nonterminal in $T_{ik}$ and $T_{(k+1)j}$ justified the decision until $i=j$.

By doing so, from nonterminal $S$ in $T_{1n}$. We can locate the proper grammar symbol in $T_{1k}$ and $T_{(k+1)j}$, until we get $T_{ii}$, where we conclude the nonterminal has a production body $a_i$. Since the conclusion must reach $n$ times, so it will cost $O(n)$ time.

Consider the total amount of locate grammar symbol when $i\ne j$. Prove that such a locate procedure of $T_{ij}$ won’t continue more than $j-i$ times by induction. For $j-i\le 1$. The only possible locate (if exists) is $T_{ii}$ nad $T_{jj}$. For $j-i=n+1$ and assume it holds for $j-i\le n$. Locate $T_{ik}$ and $T_{(k+1)j}$ with one time. And total amount of locate will be $\le (k-i)+(j-k-1)+1=j-i=n$. And this indicate all locate will cost $O(n)$ time.

Add all procedure, the total time complexity is $O(n)$.

## Problem 11

### Problem Description

 Modify your algorithm of Exercise 4.4.9 so that it will find, for any string, the smallest number of insert, delete, and mutate errors (each error a single character) needed to turn the string into a string in the language of the underlying grammar.

### Solution

1. Calculate minimum modification numbers of $a_i$ to each nonterminal.
    1. Initially let $n=1$ represents the minimum length of remaining nonterminal. If some nonterminal has productions composed by only terminals. Preserve the shortest one and eliminate others, and one production have $a_i$ in its body has a higher precedence.
    2. Estimate the lower bound of production bodies with nonterminal. And eliminate it if the estimated lower bound is higher than existed productions composed by only terminals.
    3. If there’s some nonterminal can’t be expressed only as composition of terminals, let $n$ increment by 1 and go back to (a).
    4. Calculate the obvious minumum modification numbers.
2. Do as the same sequence of Exercise 4.4.9. For every entry $T_{ij}$ do the following:
    1. For each production of a nonterminal. If the production is of the form $A\rightarrow a$. Calculate the obvious minimum modification numbers $t_1$.
    2. For each production of a nonterminal. If the produciton is of the form $A\rightarrow BC$, then check every $i\le k<j$, add the minimum modification number of $a_i\cdots a_k$ to $B$ and the minimum modification number of $a_{k+1}\cdots a_j$ to $C$. And take the minimum number of those possbilities as $t_2$.
    3. Find the minimum of $t_1$ and $t_2$ (they are sets) as the minimum modifcation number from $a_i\cdots a_j$ to the nonterminal. And repeat until all nonterminal is calculated for this entry.
3. Check $T_{1n}$ for minimum modification numbers to $S$.

## Problem 12

### Problem Description

In Fig. 4.24 is a grammar for certain statements. You may take $e$ and $s$ to be terminals standing for conditional expressions and “other statements,” respectively. If we resolve the conflict regarding expansion of the optional “else” (nonterminal *stmtTail*) by preferring to consume an **else** from the input whenever we see one, we can build a predictive parser for this grammar. Using the idea of synchronizing symbols described in Section 4.4.5:

a) Build an error-correcting predictive parsing table for the grammar.

b) Show the behavior of your parser on the following inputs:

​	(i) **if** $e$ **then** $s$ ; **if** $e$ **then** $s$ **end**

​	(ii) **while** $e$ **do begin** $s$ ; **if** $e$ **then** $s$ ; **end**

![](D:\Latex Project\课后习题\EN-Compilers, Principles, Techniques, and Tools\imgs\Exercises 4.4\image-20241026011620001.png)

### Solution

#### a)

Consider all productions begin with terminal or is $\epsilon$. Then

|            | FIRST                                             |
| ---------- | ------------------------------------------------- |
| $stmt$     | $\{\textbf{if},\textbf{while},\textbf{begin},s\}$ |
| $stmtTail$ | $\{\textbf{else},\epsilon\}$                      |
| $list$     |                                                   |
| $listTail$ | $\{;,\epsilon\}$                                  |

Consider $list\rightarrow stmt\;listTail$. This means FIRST($list$) contains FIRST($stmt$).

|            | FIRST                                             |
| ---------- | ------------------------------------------------- |
| $stmt$     | $\{\textbf{if},\textbf{while},\textbf{begin},s\}$ |
| $stmtTail$ | $\{\textbf{else},\epsilon\}$                      |
| $list$     | $\{\textbf{if},\textbf{while},\textbf{begin},s\}$ |
| $listTail$ | $\{;,\epsilon\}$                                  |

Consider all nonterminals followed by terminal, and add \$ to FOLLOW($stmt$):

|            | FOLLOW             |
| ---------- | ------------------ |
| $stmt$     | $\{\$\}$           |
| $stmtTail$ |                    |
| $list$     | $\{\textbf{end}\}$ |
| $listTail$ |                    |

For $listTail\rightarrow;list$. This means FOLLOW($list$) contains FOLLOW($listTail$). For $list\rightarrow stmt\;listTail$. This means FOLLOW($listTail$) contains FOLLOW($list$). For $stmtTail\rightarrow\textbf{else }stmt$. This means FOLLOW($stmt$) contains FOLLOW($stmtTail$). For $stmt\rightarrow\textbf{if }e\textbf{ then }stmt\;stmtTail$. This means FOLLOW($stmtTail$) contains FOLLOW($stmt$).

|            | FOLLOW                                     |
| ---------- | ------------------------------------------ |
| $stmt$     | $\{\text{FOLLOW}(stmtTail),\$\}$           |
| $stmtTail$ | $\{\text{FOLLOW}(stmt)\}$                  |
| $list$     | $\{\textbf{end},\text{FOLLOW}(listTail)\}$ |
| $listTail$ | $\{\text{FOLLOW}(list)\}$                  |

For $list\rightarrow stmt\;listTail$. This means FOLLOW($stmt$) should contain ; and FOLLOW($list$). For $stmt\rightarrow\textbf{if }e\textbf{ then }stmt\;stmtTail$. This means FOLLOW($stmt$) should contain $\textbf{else}$.

|            | FOLLOW                                           |
| ---------- | ------------------------------------------------ |
| $stmt$     | $\{;,\textbf{else},\text{FOLLOW}(stmtTail),\$\}$ |
| $stmtTail$ | $\{\text{FOLLOW}(stmt)\}$                        |
| $list$     | $\{\textbf{end},\text{FOLLOW}(listTail)\}$       |
| $listTail$ | $\{\text{FOLLOW}(list)\}$                        |

Solve the follow table:

|            | FOLLOW                   |
| ---------- | ------------------------ |
| $stmt$     | $\{;,\textbf{else},\$\}$ |
| $stmtTail$ | $\{;,\textbf{else},\$\}$ |
| $list$     | $\{\textbf{end}\}$       |
| $listTail$ | $\{\textbf{end}\}$       |

Consider all productions begin with terminal. Then

|            | if                                                          | $e$  | then | while                                              | do   | begin                                             | end  | $s$                 | else                                    | ;                          | \$   |
| ---------- | ----------------------------------------------------------- | ---- | ---- | -------------------------------------------------- | ---- | ------------------------------------------------- | ---- | ------------------- | --------------------------------------- | -------------------------- | ---- |
| $stmt$     | $stmt\rightarrow\textbf{if }e\textbf{ then }stmt\;stmtTail$ |      |      | $stmt\rightarrow\textbf{while }e\textbf{ do }stmt$ |      | $stmt\rightarrow\textbf{begin }list\textbf{ end}$ |      | $stmt\rightarrow s$ |                                         |                            |      |
| $stmtTail$ |                                                             |      |      |                                                    |      |                                                   |      |                     | $stmtTail\rightarrow\textbf{else }stmt$ |                            |      |
| $list$     |                                                             |      |      |                                                    |      |                                                   |      |                     |                                         |                            |      |
| $listTail$ |                                                             |      |      |                                                    |      |                                                   |      |                     |                                         | $listTail\rightarrow;list$ |      |

For $list\rightarrow stmt\;listTail$, we need to add it to $\textbf{if},\textbf{while},\textbf{begin},s$:

|            | if                                                          | $e$  | then | while                                              | do   | begin                                             | end  | $s$                              | else                                    | ;                          | \$   |
| ---------- | ----------------------------------------------------------- | ---- | ---- | -------------------------------------------------- | ---- | ------------------------------------------------- | ---- | -------------------------------- | --------------------------------------- | -------------------------- | ---- |
| $stmt$     | $stmt\rightarrow\textbf{if }e\textbf{ then }stmt\;stmtTail$ |      |      | $stmt\rightarrow\textbf{while }e\textbf{ do }stmt$ |      | $stmt\rightarrow\textbf{begin }list\textbf{ end}$ |      | $stmt\rightarrow s$              |                                         |                            |      |
| $stmtTail$ |                                                             |      |      |                                                    |      |                                                   |      |                                  | $stmtTail\rightarrow\textbf{else }stmt$ |                            |      |
| $list$     | $list\rightarrow stmt\;listTail$                            |      |      | $list\rightarrow stmt\;listTail$                   |      | $list\rightarrow stmt\;listTail$                  |      | $list\rightarrow stmt\;listTail$ |                                         |                            |      |
| $listTail$ |                                                             |      |      |                                                    |      |                                                   |      |                                  |                                         | $listTail\rightarrow;list$ |      |

For $stmtTail\rightarrow\epsilon$, we need to add it to $;,\textbf{else},\$$:

|            | if                                                          | $e$  | then | while                                              | do   | begin                                             | end  | $s$                              | else                                    | ;                             | \$                            |
| ---------- | ----------------------------------------------------------- | ---- | ---- | -------------------------------------------------- | ---- | ------------------------------------------------- | ---- | -------------------------------- | --------------------------------------- | ----------------------------- | ----------------------------- |
| $stmt$     | $stmt\rightarrow\textbf{if }e\textbf{ then }stmt\;stmtTail$ |      |      | $stmt\rightarrow\textbf{while }e\textbf{ do }stmt$ |      | $stmt\rightarrow\textbf{begin }list\textbf{ end}$ |      | $stmt\rightarrow s$              |                                         |                               |                               |
| $stmtTail$ |                                                             |      |      |                                                    |      |                                                   |      |                                  | $stmtTail\rightarrow\textbf{else }stmt$ | $stmtTail\rightarrow\epsilon$ | $stmtTail\rightarrow\epsilon$ |
|            |                                                             |      |      |                                                    |      |                                                   |      |                                  | $stmtTail\rightarrow\epsilon$           |                               |                               |
| $list$     | $list\rightarrow stmt\;listTail$                            |      |      | $list\rightarrow stmt\;listTail$                   |      | $list\rightarrow stmt\;listTail$                  |      | $list\rightarrow stmt\;listTail$ |                                         |                               |                               |
| $listTail$ |                                                             |      |      |                                                    |      |                                                   |      |                                  |                                         | $listTail\rightarrow;list$    |                               |

For $listTail\rightarrow\epsilon$, we need to add it to $\textbf{end}$:

|            | if                                                          | $e$  | then | while                                              | do   | begin                                             | end                           | $s$                              | else                                    | ;                             | \$                            |
| ---------- | ----------------------------------------------------------- | ---- | ---- | -------------------------------------------------- | ---- | ------------------------------------------------- | ----------------------------- | -------------------------------- | --------------------------------------- | ----------------------------- | ----------------------------- |
| $stmt$     | $stmt\rightarrow\textbf{if }e\textbf{ then }stmt\;stmtTail$ |      |      | $stmt\rightarrow\textbf{while }e\textbf{ do }stmt$ |      | $stmt\rightarrow\textbf{begin }list\textbf{ end}$ |                               | $stmt\rightarrow s$              |                                         |                               |                               |
| $stmtTail$ |                                                             |      |      |                                                    |      |                                                   |                               |                                  | $stmtTail\rightarrow\textbf{else }stmt$ | $stmtTail\rightarrow\epsilon$ | $stmtTail\rightarrow\epsilon$ |
|            |                                                             |      |      |                                                    |      |                                                   |                               |                                  | $stmtTail\rightarrow\epsilon$           |                               |                               |
| $list$     | $list\rightarrow stmt\;listTail$                            |      |      | $list\rightarrow stmt\;listTail$                   |      | $list\rightarrow stmt\;listTail$                  |                               | $list\rightarrow stmt\;listTail$ |                                         |                               |                               |
| $listTail$ |                                                             |      |      |                                                    |      |                                                   | $listTail\rightarrow\epsilon$ |                                  |                                         | $listTail\rightarrow;list$    |                               |

Add synch into the table by considering FIRST and FOLLOW:

|            | if                                                          | $e$  | then | while                                              | do   | begin                                             | end                           | $s$                              | else                                    | ;                             | \$                            |
| ---------- | ----------------------------------------------------------- | ---- | ---- | -------------------------------------------------- | ---- | ------------------------------------------------- | ----------------------------- | -------------------------------- | --------------------------------------- | ----------------------------- | ----------------------------- |
| $stmt$     | $stmt\rightarrow\textbf{if }e\textbf{ then }stmt\;stmtTail$ |      |      | $stmt\rightarrow\textbf{while }e\textbf{ do }stmt$ |      | $stmt\rightarrow\textbf{begin }list\textbf{ end}$ |                               | $stmt\rightarrow s$              | synch                                   | synch                         | synch                         |
| $stmtTail$ |                                                             |      |      |                                                    |      |                                                   |                               |                                  | $stmtTail\rightarrow\textbf{else }stmt$ | $stmtTail\rightarrow\epsilon$ | $stmtTail\rightarrow\epsilon$ |
|            |                                                             |      |      |                                                    |      |                                                   |                               |                                  | $stmtTail\rightarrow\epsilon$           |                               |                               |
| $list$     | $list\rightarrow stmt\;listTail$                            |      |      | $list\rightarrow stmt\;listTail$                   |      | $list\rightarrow stmt\;listTail$                  | synch                         | $list\rightarrow stmt\;listTail$ |                                         |                               |                               |
| $listTail$ |                                                             |      |      |                                                    |      |                                                   | $listTail\rightarrow\epsilon$ |                                  |                                         | $listTail\rightarrow;list$    |                               |

Eliminate the conflict:

|            | if                                                          | $e$  | then | while                                              | do   | begin                                             | end                           | $s$                              | else                                    | ;                             | \$                            |
| ---------- | ----------------------------------------------------------- | ---- | ---- | -------------------------------------------------- | ---- | ------------------------------------------------- | ----------------------------- | -------------------------------- | --------------------------------------- | ----------------------------- | ----------------------------- |
| $stmt$     | $stmt\rightarrow\textbf{if }e\textbf{ then }stmt\;stmtTail$ |      |      | $stmt\rightarrow\textbf{while }e\textbf{ do }stmt$ |      | $stmt\rightarrow\textbf{begin }list\textbf{ end}$ |                               | $stmt\rightarrow s$              | synch                                   | synch                         | synch                         |
| $stmtTail$ |                                                             |      |      |                                                    |      |                                                   |                               |                                  | $stmtTail\rightarrow\textbf{else }stmt$ | $stmtTail\rightarrow\epsilon$ | $stmtTail\rightarrow\epsilon$ |
| $list$     | $list\rightarrow stmt\;listTail$                            |      |      | $list\rightarrow stmt\;listTail$                   |      | $list\rightarrow stmt\;listTail$                  | synch                         | $list\rightarrow stmt\;listTail$ |                                         |                               |                               |
| $listTail$ |                                                             |      |      |                                                    |      |                                                   | $listTail\rightarrow\epsilon$ |                                  |                                         | $listTail\rightarrow;list$    ||

#### b)

(i) 
$$
stmt\Rightarrow\textbf{if }e\textbf{ then }stmt\;stmtTail\Rightarrow \textbf{if }e\textbf{ then }s\;stmtTail\Rightarrow \textbf{if }e\textbf{ then }s\;
$$
Then $[list,\textbf{end}]$ is synch, which means the parser will pass this round and check $[list,\$]$, which means a syntax error.

(ii)
$$
stmt\Rightarrow \textbf{while }e\textbf{ do }stmt\Rightarrow \textbf{while }e\textbf{ do begin }list\textbf{ end}\Rightarrow \textbf{while }e\textbf{ do begin }stmt\;listTail\textbf{ end}\\
\Rightarrow \textbf{while }e\textbf{ do begin }s\;listTail\textbf{ end}\Rightarrow \textbf{while }e\textbf{ do begin }s\;;list\textbf{ end}\Rightarrow \textbf{while }e\textbf{ do begin }s\;;stmt\;listTail\textbf{ end}\\
\Rightarrow \textbf{while }e\textbf{ do begin }s\;;\textbf{if }e\textbf{ then }stmt\;stmtTail\;listTail\textbf{ end}\Rightarrow \textbf{while }e\textbf{ do begin }s\;;\textbf{if }e\textbf{ then }s\;stmtTail\;listTail\textbf{ end}\\
\Rightarrow \textbf{while }e\textbf{ do begin }s\;;\textbf{if }e\textbf{ then }s\;listTail\textbf{ end}\Rightarrow \textbf{while }e\textbf{ do begin }s\;;\textbf{if }e\textbf{ then }s\;;list\textbf{ end}
$$
$list$ then escape the $\textbf{end}$, and then to $\$$, which will lead to syntax error.