# Exercises 4.7

## Problem 1

### Problem Description

Construct the

a) canonical LR, and

b) LALR

sets of items for the grammar $S\rightarrow SS+\;|\;SS*\;|\;a$ of Exercise 4.2.1.

### Solution

#### a

The augmented grammar is
$$
S'\rightarrow S\\
S\rightarrow SS+\;|\;SS*\;|\;a
$$
First, construct the FIRST table

|      | FIRST   |
| ---- | ------- |
| $S’$ | $\{a\}$ |
| $S$  | $\{a\}$ |

And then construct the LR table directly

| Kernel                                                       | Nonkernel                                                    | $S$                                                          | $+$                           | $*$                           | $a$                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------- | ----------------------------- | --------------------------- |
| $S’\rightarrow\cdot S,\$$                                    | $S\rightarrow\cdot SS+,a/\$\\S\rightarrow\cdot SS*,a/\$\\S\rightarrow \cdot a,a/\$$ | $S’\rightarrow S\cdot,\$\\S\rightarrow S\cdot S+,a/\$\\S\rightarrow S\cdot S*,a/\$$ |                               |                               | $S\rightarrow a\cdot,a/\$$  |
|                                                              |                                                              |                                                              |                               |                               |                             |
| $S’\rightarrow S\cdot,\$\\S\rightarrow S\cdot S+,a/\$\\S\rightarrow S\cdot S*,a/\$$ | $S\rightarrow\cdot SS+,+/*/a\\S\rightarrow\cdot SS*,+/*/a\\S\rightarrow\cdot a,+/*/a$ | $S\rightarrow SS\cdot +,a/\$\\S\rightarrow SS\cdot *,a/\$\\S\rightarrow S\cdot S+,+/*/a\\S\rightarrow S\cdot S*,+/*/a$ |                               |                               | $S\rightarrow a\cdot,+/*/a$ |
|                                                              |                                                              |                                                              |                               |                               |                             |
| $S\rightarrow SS\cdot +,a/\$\\S\rightarrow SS\cdot *,a/\$\\S\rightarrow S\cdot S+,+/*/a\\S\rightarrow S\cdot S*,+/*/a$ | $S\rightarrow\cdot SS+,+/*/a\\S\rightarrow\cdot SS*,+/*/a\\S\rightarrow\cdot a,+/*/a$ | $S\rightarrow SS\cdot+,+/*/a\\S\rightarrow SS\cdot *,+/*/a\\S\rightarrow S\cdot S+,+/*/a\\S\rightarrow S\cdot S*,+/*/a$ | $S\rightarrow SS+\cdot,a/\$$  | $S\rightarrow SS*\cdot,a/\$$  | $S\rightarrow a\cdot,+/*/a$ |
|                                                              |                                                              |                                                              |                               |                               |                             |
| $S\rightarrow SS\cdot+,+/*/a\\S\rightarrow SS\cdot *,+/*/a\\S\rightarrow S\cdot S+,+/*/a\\S\rightarrow S\cdot S*,+/*/a$ | $S\rightarrow\cdot SS+,+/*/a\\S\rightarrow\cdot SS*,+/*/a\\S\rightarrow\cdot a,+/*/a$ | $S\rightarrow SS\cdot+,+/*/a\\S\rightarrow SS\cdot *,+/*/a\\S\rightarrow S\cdot S+,+/*/a\\S\rightarrow S\cdot S*,+/*/a$ | $S\rightarrow SS+\cdot,+/*/a$ | $S\rightarrow SS*\cdot,+/*/a$ | $S\rightarrow a\cdot,+/*/a$ |
|                                                              |                                                              |                                                              |                               |                               |                             |
| $S\rightarrow a\cdot,a/\$$                                   |                                                              |                                                              |                               |                               |                             |
|                                                              |                                                              |                                                              |                               |                               |                             |
| $S\rightarrow a\cdot,+/*/a$                                  |                                                              |                                                              |                               |                               |                             |
|                                                              |                                                              |                                                              |                               |                               |                             |
| $S\rightarrow SS+\cdot,a/\$$                                 |                                                              |                                                              |                               |                               |                             |
|                                                              |                                                              |                                                              |                               |                               |                             |
| $S\rightarrow SS*\cdot,a/\$$                                 |                                                              |                                                              |                               |                               |                             |
|                                                              |                                                              |                                                              |                               |                               |                             |
| $S\rightarrow SS+\cdot,+/*/a$                                |                                                              |                                                              |                               |                               |                             |
|                                                              |                                                              |                                                              |                               |                               |                             |
| $S\rightarrow SS*\cdot,+/*/a$                                |                                                              |                                                              |                               |                               |                             |

The canonical LR items are calculated by merging the kernel and nonkernel items.

#### b

We can derive those items directly by the kernel items in a):
$$
S'\rightarrow\cdot S,\$\\\\S’\rightarrow S\cdot,\$\\S\rightarrow S\cdot S+,a/\$\\S\rightarrow S\cdot S*,a/\$\\\\S\rightarrow SS\cdot +,+/*/a/\$\\S\rightarrow SS\cdot *,+/*/a/\$\\S\rightarrow S\cdot S+,+/*/a\\S\rightarrow S\cdot S*,+/*/a\\\\S\rightarrow a\cdot,+/*/a/\$\\\\S\rightarrow SS+\cdot,+/*/a/\$\\\\S\rightarrow SS*\cdot,+/*/a/\$
$$

## Problem 2

### Problem Description

Repeat Exercise 4.7.1 for each of the (augmented) grammars of Exercise 4.2.2(a)-(g).

### Solution

#### a

The augmented grammar is
$$
S'\rightarrow S\\
S\rightarrow 0S1\;|\;01
$$
First, construct the FIRST table

|      | FIRST   |
| ---- | ------- |
| $S'$ | $\{0\}$ |
| $S$  | $\{0\}$ |

And then construct the LR table directly

| Kernel                                                | Nonkernel                                           | $S$                         | 0                                                     | 1                          |
| ----------------------------------------------------- | --------------------------------------------------- | --------------------------- | ----------------------------------------------------- | -------------------------- |
| $S’\rightarrow\cdot S,\$$                             | $S\rightarrow\cdot 0S1,\$\\S\rightarrow\cdot 01,\$$ | $S'\rightarrow S\cdot,\$$   | $S\rightarrow 0\cdot S1,\$\\S\rightarrow 0\cdot 1,\$$ |                            |
|                                                       |                                                     |                             |                                                       |                            |
| $S\rightarrow 0\cdot S1,\$\\S\rightarrow 0\cdot 1,\$$ | $S\rightarrow\cdot 0S1,1\\S\rightarrow\cdot 01,1$   | $S\rightarrow 0S\cdot 1,\$$ | $S\rightarrow 0\cdot S1,1\\S\rightarrow0\cdot 1,1$    | $S\rightarrow01\cdot,\$$   |
|                                                       |                                                     |                             |                                                       |                            |
| $S\rightarrow 0S\cdot 1,\$$                           |                                                     |                             |                                                       | $S\rightarrow 0S1\cdot,\$$ |
|                                                       |                                                     |                             |                                                       |                            |
| $S\rightarrow 0\cdot S1,1\\S\rightarrow0\cdot 1,1$    | $S\rightarrow\cdot 0S1,1\\S\rightarrow\cdot 01,1$   | $S\rightarrow 0S\cdot1,1$   | $S\rightarrow0\cdot S1,1\\S\rightarrow 0\cdot 1,1$    | $S\rightarrow 01\cdot,1$   |
|                                                       |                                                     |                             |                                                       |                            |
| $S\rightarrow 0S\cdot1,1$                             |                                                     |                             |                                                       | $S\rightarrow 0S1\cdot,1$  |
|                                                       |                                                     |                             |                                                       |                            |
| $S'\rightarrow S\cdot,\$$                             |                                                     |                             |                                                       |                            |
|                                                       |                                                     |                             |                                                       |                            |
| $S\rightarrow01\cdot,\$$                              |                                                     |                             |                                                       |                            |
|                                                       |                                                     |                             |                                                       |                            |
| $S\rightarrow 0S1\cdot,\$$                            |                                                     |                             |                                                       |                            |
|                                                       |                                                     |                             |                                                       |                            |
| $S\rightarrow 01\cdot,1$                              |                                                     |                             |                                                       |                            |
|                                                       |                                                     |                             |                                                       |                            |
| $S\rightarrow 0S1\cdot,1$                             |                                                     |                             |                                                       |                            |

And the LALR items are
$$
S'\rightarrow\cdot S,\$\\\\
S\rightarrow 0\cdot S1,1/\$\\S\rightarrow 0\cdot 1,1/\$\\\\
S\rightarrow 0S\cdot 1,1/\$\\\\
S'\rightarrow S\cdot,\$\\\\
S\rightarrow01\cdot,1/\$\\\\
S\rightarrow 0S1\cdot,1/\$
$$

#### b

The augmented grammar is
$$
S'\rightarrow S\\
S\rightarrow +SS\;|\;*SS\;|\;a
$$
First, construct the FIRST table

|      | FIRST       |
| ---- | ----------- |
| $S$  | $\{+,*,a\}$ |

And then construct the LR table directly

| Kernel                         | Nonkernel                                                    | $S$                            | $+$                            | $*$                            | $a$                         |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ | --------------------------- |
| $S'\rightarrow\cdot S,\$$      | $S\rightarrow\cdot +SS,\$\\S\rightarrow\cdot *SS,\$\\S\rightarrow\cdot a,\$$ | $S'\rightarrow S\cdot,\$$      | $S\rightarrow +\cdot SS,\$$    | $S\rightarrow *\cdot SS,\$$    | $S\rightarrow a\cdot,\$$    |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow +\cdot SS,\$$    | $S\rightarrow\cdot +SS,+/*/a\\S\rightarrow\cdot *SS,+/*/a\\S\rightarrow \cdot a,+/*/a$ | $S\rightarrow +S\cdot S,\$$    | $S\rightarrow +\cdot SS,+/*/a$ | $S\rightarrow *\cdot SS,+/*/a$ | $S\rightarrow a\cdot,+/*/a$ |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow *\cdot SS,\$$    | $S\rightarrow\cdot +SS,+/*/a\\S\rightarrow\cdot *SS,+/*/a\\S\rightarrow \cdot a,+/*/a$ | $S\rightarrow *S\cdot S,\$$    | $S\rightarrow +\cdot SS,+/*/a$ | $S\rightarrow *\cdot SS,+/*/a$ | $S\rightarrow a\cdot,+/*/a$ |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow +S\cdot S,\$$    | $S\rightarrow\cdot +SS,\$\\S\rightarrow\cdot *SS,\$\\S\rightarrow\cdot a,\$$ | $S\rightarrow +SS\cdot,\$$     | $S\rightarrow +\cdot SS,\$$    | $S\rightarrow *\cdot SS,\$$    | $S\rightarrow a\cdot,\$$    |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow +\cdot SS,+/*/a$ | $S\rightarrow\cdot +SS,+/*/a\\S\rightarrow\cdot *SS,+/*/a\\S\rightarrow \cdot a,+/*/a$ | $S\rightarrow +S\cdot S,+/*/a$ | $S\rightarrow +\cdot SS,+/*/a$ | $S\rightarrow *\cdot SS,+/*/a$ | $S\rightarrow a\cdot,+/*/a$ |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow *\cdot SS,+/*/a$ | $S\rightarrow\cdot +SS,+/*/a\\S\rightarrow\cdot *SS,+/*/a\\S\rightarrow \cdot a,+/*/a$ | $S\rightarrow *S\cdot S,+/*/a$ | $S\rightarrow +\cdot SS,+/*/a$ | $S\rightarrow *\cdot SS,+/*/a$ | $S\rightarrow a\cdot,+/*/a$ |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow *S\cdot S,\$$    | $S\rightarrow\cdot +SS,\$\\S\rightarrow\cdot *SS,\$\\S\rightarrow\cdot a,\$$ | $S\rightarrow *SS\cdot,\$$     | $S\rightarrow +\cdot SS,\$$    | $S\rightarrow *\cdot SS,\$$    | $S\rightarrow a\cdot,\$$    |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow +S\cdot S,+/*/a$ | $S\rightarrow\cdot +SS,+/*/a\\S\rightarrow\cdot *SS,+/*/a\\S\rightarrow \cdot a,+/*/a$ | $S\rightarrow +SS\cdot,+/*/a$  | $S\rightarrow +\cdot SS,+/*/a$ | $S\rightarrow *\cdot SS,+/*/a$ | $S\rightarrow a\cdot,+/*/a$ |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow *S\cdot S,+/*/a$ | $S\rightarrow\cdot +SS,+/*/a\\S\rightarrow\cdot *SS,+/*/a\\S\rightarrow \cdot a,+/*/a$ | $S\rightarrow *SS\cdot,+/*/a$  | $S\rightarrow +\cdot SS,+/*/a$ | $S\rightarrow *\cdot SS,+/*/a$ | $S\rightarrow a\cdot,+/*/a$ |
|                                |                                                              |                                |                                |                                |                             |
| $S'\rightarrow S\cdot,\$$      |                                                              |                                |                                |                                |                             |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow a\cdot,\$$       |                                                              |                                |                                |                                |                             |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow a\cdot,+/*/a$    |                                                              |                                |                                |                                |                             |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow +SS\cdot,\$$     |                                                              |                                |                                |                                |                             |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow *SS\cdot,\$$     |                                                              |                                |                                |                                |                             |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow +SS\cdot,+/*/a$  |                                                              |                                |                                |                                |                             |
|                                |                                                              |                                |                                |                                |                             |
| $S\rightarrow *SS\cdot,+/*/a$  |                                                              |                                |                                |                                |                             |

And the LALR items are
$$
S'\rightarrow\cdot S,\$\\\\
S\rightarrow +\cdot SS,+/*/a/\$\\\\
S\rightarrow *\cdot SS,+/*/a/\$\\\\
S\rightarrow +S\cdot S,+/*/a/\$\\\\
S\rightarrow *S\cdot S,+/*/a/\$\\\\
S'\rightarrow S\cdot,\$\\\\
S\rightarrow +SS\cdot,+/*/a/\$\\\\
S\rightarrow *SS\cdot,+/*/a/\$
$$

#### c

The augmented grammar is
$$
S'\rightarrow S\\
S\rightarrow S(S)S\;|\;\epsilon
$$
First, construct the FIRST table

|      | FIRST            |
| ---- | ---------------- |
| $S$  | $\{(,\epsilon\}$ |

And then construct the LR table directly

| Kernel                                                       | Nonkernel                                                | $S$                                                          | (                               | )                               |
| ------------------------------------------------------------ | -------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------- | ------------------------------- |
| $S’\rightarrow\cdot S,\$$                                    | $S\rightarrow\cdot S(S)S,\$/(\\S\rightarrow\cdot,\$/($   | $S'\rightarrow S\cdot,\$\\S\rightarrow S\cdot(S)S,\$/($      |                                 |                                 |
|                                                              |                                                          |                                                              |                                 |                                 |
| $S'\rightarrow S\cdot,\$\\S\rightarrow S\cdot(S)S,\$/($      |                                                          |                                                              | $S\rightarrow S(\cdot S)S,\$/($ |                                 |
|                                                              |                                                          |                                                              |                                 |                                 |
| $S\rightarrow S(\cdot S)S,\$/($                              | $S\rightarrow\cdot S(S)S,(/)\\S\rightarrow\cdot,(/)$     | $S\rightarrow S(S\cdot)S,\$/(\\S\rightarrow S\cdot(S)S,(/)$  |                                 |                                 |
|                                                              |                                                          |                                                              |                                 |                                 |
| $S\rightarrow S(S\cdot)S,\$/(\\S\rightarrow S\cdot(S)S,(/)$  |                                                          |                                                              | $S\rightarrow S(\cdot S)S,(/)$  | $S\rightarrow S(S)\cdot S,\$/($ |
|                                                              |                                                          |                                                              |                                 |                                 |
| $S\rightarrow S(\cdot S)S,(/)$                               | $S\rightarrow\cdot S(S)S,(/)\\S\rightarrow\cdot,(/)$     | $S\rightarrow S(S\cdot)S,(/)\\S\rightarrow S\cdot(S)S,(/)$   |                                 |                                 |
|                                                              |                                                          |                                                              |                                 |                                 |
| $S\rightarrow S(S)\cdot S,\$/($                              | $$S\rightarrow\cdot S(S)S,\$/(\\S\rightarrow\cdot,\$/($$ | $S\rightarrow S(S)S\cdot,\$/(\\S\rightarrow S\cdot(S)S,\$/($ |                                 |                                 |
|                                                              |                                                          |                                                              |                                 |                                 |
| $S\rightarrow S(S\cdot)S,(/)\\S\rightarrow S\cdot(S)S,(/)$   |                                                          |                                                              | $S\rightarrow S(\cdot S)S,(/)$  | $S\rightarrow S(S)\cdot S,(/)$  |
|                                                              |                                                          |                                                              |                                 |                                 |
| $S\rightarrow S(S)S\cdot,\$/(\\S\rightarrow S\cdot(S)S,\$/($ |                                                          |                                                              | $S\rightarrow S(\cdot S)S,\$/($ |                                 |
|                                                              |                                                          |                                                              |                                 |                                 |
| $S\rightarrow S(S)\cdot S,(/)$                               | $S\rightarrow\cdot S(S)S,(/)\\S\rightarrow\cdot,(/)$     | $S\rightarrow S(S)S\cdot,(/)\\S\rightarrow S\cdot(S)S,(/)$   |                                 |                                 |
|                                                              |                                                          |                                                              |                                 |                                 |
| $S\rightarrow S(S)S\cdot,(/)\\S\rightarrow S\cdot(S)S,(/)$   |                                                          |                                                              | $S\rightarrow S(\cdot S)S,(/)$  |                                 |

And the LALR items are
$$
S’\rightarrow\cdot S,\$\\\\
S'\rightarrow S\cdot,\$\\S\rightarrow S\cdot(S)S,\$/(\\\\
S\rightarrow S(\cdot S)S,\$/(/)\\\\
S\rightarrow S(S\cdot)S,\$/(/)\\S\rightarrow S\cdot(S)S,(/)\\\\
S\rightarrow S(S)\cdot S,\$/(/)\\\\
S\rightarrow S(S)S\cdot,\$/(/)\\S\rightarrow S\cdot(S)S,\$/(/)
$$

#### d

The augmented grammar is
$$
S'\rightarrow S\\
S\rightarrow S+S\;|\;SS\;|\;(S)\;|\;S*\;|\;a
$$
First, construct the FIRST table

|      | FIRST     |
| ---- | --------- |
| $S$  | $\{(,a\}$ |

And then construct the LR table directly

| Kernel                                                       | Nonkernel                                                    | $S$                                                          | $+$                                 | $($                                 | $)$                               | $*$                               | $a$                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------- | ----------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- |
| $S’\rightarrow \cdot S,\$$                                   | $S\rightarrow\cdot S+S,\$/+/*/(/a\\S\rightarrow\cdot SS,\$/+/*/(/a\\S\rightarrow\cdot(S),\$/+/*/(/a\\S\rightarrow\cdot S*,\$/+/*/(/a\\S\rightarrow\cdot a,\$/+/*/(/a$ | $S'\rightarrow S\cdot,\$\\S\rightarrow S\cdot+S,\$/+/*/(/a\\S\rightarrow S\cdot S,\$/+/*/(/a\\S\rightarrow S\cdot *,\$/+/*/(/a$ |                                     | $S\rightarrow (\cdot S),\$/+/*/(/a$ |                                   |                                   | $S\rightarrow a\cdot ,\$/+/*/(/a$ |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S'\rightarrow S\cdot,\$\\S\rightarrow S\cdot+S,\$/+/*/(/a\\S\rightarrow S\cdot S,\$/+/*/(/a\\S\rightarrow S\cdot *,\$/+/*/(/a$ | $S\rightarrow\cdot S+S,\$/+/*/(/a\\S\rightarrow\cdot SS,\$/+/*/(/a\\S\rightarrow\cdot(S),\$/+/*/(/a\\S\rightarrow\cdot S*,\$/+/*/(/a\\S\rightarrow\cdot a,\$/+/*/(/a$ | $S\rightarrow SS\cdot,\$/+/*/(/a\\S\rightarrow S\cdot+S,\$/+/*/(/a\\S\rightarrow S\cdot S,\$/+/*/(/a\\S\rightarrow S\cdot *,\$/+/*/(/a$ | $S\rightarrow S+\cdot S,\$/+/*/(/a$ | $S\rightarrow (\cdot S),\$/+/*/(/a$ |                                   | $S\rightarrow S*\cdot,\$/+/*/(/a$ | $S\rightarrow a\cdot ,\$/+/*/(/a$ |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow (\cdot S),\$/+/*/(/a$                          | $S\rightarrow\cdot S+S,)/+/*/(/a\\S\rightarrow\cdot SS,)/+/*/(/a\\S\rightarrow\cdot(S),)/+/*/(/a\\S\rightarrow\cdot S*,)/+/*/(/a\\S\rightarrow\cdot a,)/+/*/(/a$ | $S\rightarrow(S\cdot),\$/+/*/(/a\\S\rightarrow S\cdot+S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ |                                     | $S\rightarrow(\cdot S),)/+/*/(/a$   |                                   |                                   | $S\rightarrow a\cdot,)/+/*/(/a$   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow SS\cdot,\$/+/*/(/a\\S\rightarrow S\cdot+S,\$/+/*/(/a\\S\rightarrow S\cdot S,\$/+/*/(/a\\S\rightarrow S\cdot *,\$/+/*/(/a$ | $S\rightarrow\cdot S+S,\$/+/*/(/a\\S\rightarrow\cdot SS,\$/+/*/(/a\\S\rightarrow\cdot(S),\$/+/*/(/a\\S\rightarrow\cdot S*,\$/+/*/(/a\\S\rightarrow\cdot a,\$/+/*/(/a$ | $S\rightarrow SS\cdot,\$/+/*/(/a\\S\rightarrow S\cdot+S,\$/+/*/(/a\\S\rightarrow S\cdot S,\$/+/*/(/a\\S\rightarrow S\cdot *,\$/+/*/(/a$ | $S\rightarrow S+\cdot S,\$/+/*/(/a$ | $S\rightarrow (\cdot S),\$/+/*/(/a$ |                                   | $S\rightarrow S*\cdot,\$/+/*/(/a$ | $S\rightarrow a\cdot ,\$/+/*/(/a$ |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow S+\cdot S,\$/+/*/(/a$                          | $S\rightarrow\cdot S+S,\$/+/*/(/a\\S\rightarrow\cdot SS,\$/+/*/(/a\\S\rightarrow\cdot(S),\$/+/*/(/a\\S\rightarrow\cdot S*,\$/+/*/(/a\\S\rightarrow\cdot a,\$/+/*/(/a$ | $S\rightarrow S+S\cdot,\$/+/*/(/a\\S\rightarrow S\cdot+S,\$/+/*/(/a\\S\rightarrow S\cdot S,\$/+/*/(/a\\S\rightarrow S\cdot *,\$/+/*/(/a$ |                                     | $S\rightarrow (\cdot S),\$/+/*/(/a$ |                                   |                                   | $S\rightarrow a\cdot ,\$/+/*/(/a$ |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow(S\cdot),\$/+/*/(/a\\S\rightarrow S\cdot+S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ | $S\rightarrow\cdot S+S,)/+/*/(/a\\S\rightarrow\cdot SS,)/+/*/(/a\\S\rightarrow\cdot(S),)/+/*/(/a\\S\rightarrow\cdot S*,)/+/*/(/a\\S\rightarrow\cdot a,)/+/*/(/a$ | $S\rightarrow SS\cdot,)/+/*/(/a\\S\rightarrow S\cdot +S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ |                                     | $S\rightarrow(\cdot S),)/+/*/(/a$   | $S\rightarrow(S)\cdot,\$/+/*/(/a$ | $S\rightarrow S*\cdot,)/+/*/(/a$  | $S\rightarrow a\cdot,)/+/*/(/a$   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow(\cdot S),)/+/*/(/a$                            | $S\rightarrow\cdot S+S,)/+/*/(/a\\S\rightarrow\cdot SS,)/+/*/(/a\\S\rightarrow\cdot(S),)/+/*/(/a\\S\rightarrow\cdot S*,)/+/*/(/a\\S\rightarrow\cdot a,)/+/*/(/a$ | $S\rightarrow(S\cdot),)/+/*/(/a\\S\rightarrow S\cdot+S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ |                                     | $S\rightarrow(\cdot S),)/+/*/(/a$   |                                   |                                   | $S\rightarrow a\cdot,)/+/*/(/a$   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow S+S\cdot,\$/+/*/(/a\\S\rightarrow S\cdot+S,\$/+/*/(/a\\S\rightarrow S\cdot S,\$/+/*/(/a\\S\rightarrow S\cdot *,\$/+/*/(/a$ | $S\rightarrow\cdot S+S,\$/+/*/(/a\\S\rightarrow\cdot SS,\$/+/*/(/a\\S\rightarrow\cdot(S),\$/+/*/(/a\\S\rightarrow\cdot S*,\$/+/*/(/a\\S\rightarrow\cdot a,\$/+/*/(/a$ | $S\rightarrow SS\cdot,\$/+/*/(/a\\S\rightarrow S\cdot+S,\$/+/*/(/a\\S\rightarrow S\cdot S,\$/+/*/(/a\\S\rightarrow S\cdot *,\$/+/*/(/a$ | $S\rightarrow S+\cdot S,\$/+/*/(/a$ | $S\rightarrow (\cdot S),\$/+/*/(/a$ |                                   | $S\rightarrow S*\cdot,\$/+/*/(/a$ | $S\rightarrow a\cdot ,\$/+/*/(/a$ |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow SS\cdot,)/+/*/(/a\\S\rightarrow S\cdot +S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ | $S\rightarrow\cdot S+S,)/+/*/(/a\\S\rightarrow\cdot SS,)/+/*/(/a\\S\rightarrow\cdot(S),)/+/*/(/a\\S\rightarrow\cdot S*,)/+/*/(/a\\S\rightarrow\cdot a,)/+/*/(/a$ | $S\rightarrow SS\cdot,)/+/*/(/a\\S\rightarrow S\cdot +S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ | $S\rightarrow S+\cdot S,)/+/*/(/a$  | $S\rightarrow(\cdot S),)/+/*/(/a$   |                                   | $S\rightarrow S*\cdot,)/+/*/(/a$  | $S\rightarrow a\cdot,)/+/*/(/a$   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow(S\cdot),)/+/*/(/a\\S\rightarrow S\cdot+S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ | $S\rightarrow\cdot S+S,)/+/*/(/a\\S\rightarrow\cdot SS,)/+/*/(/a\\S\rightarrow\cdot(S),)/+/*/(/a\\S\rightarrow\cdot S*,)/+/*/(/a\\S\rightarrow\cdot a,)/+/*/(/a$ | $S\rightarrow SS\cdot,)/+/*/(/a\\S\rightarrow S\cdot +S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ | $S\rightarrow S+\cdot S,)/+/*/(/a$  | $S\rightarrow(\cdot S),)/+/*/(/a$   | $S\rightarrow(S)\cdot,)/+/*/(/a$  | $S\rightarrow S*\cdot,)/+/*/(/a$  | $S\rightarrow a\cdot,)/+/*/(/a$   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow S+\cdot S,)/+/*/(/a$                           | $S\rightarrow\cdot S+S,)/+/*/(/a\\S\rightarrow\cdot SS,)/+/*/(/a\\S\rightarrow\cdot(S),)/+/*/(/a\\S\rightarrow\cdot S*,)/+/*/(/a\\S\rightarrow\cdot a,)/+/*/(/a$ | $S\rightarrow S+S\cdot,)/+/*/(/a\\S\rightarrow S\cdot +S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ |                                     | $S\rightarrow(\cdot S),)/+/*/(/a$   |                                   |                                   | $S\rightarrow a\cdot,)/+/*/(/a$   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow S+S\cdot,)/+/*/(/a\\S\rightarrow S\cdot +S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ | $S\rightarrow\cdot S+S,)/+/*/(/a\\S\rightarrow\cdot SS,)/+/*/(/a\\S\rightarrow\cdot(S),)/+/*/(/a\\S\rightarrow\cdot S*,)/+/*/(/a\\S\rightarrow\cdot a,)/+/*/(/a$ | $S\rightarrow SS\cdot,)/+/*/(/a\\S\rightarrow S\cdot +S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a$ | $S\rightarrow S+\cdot S,)/+/*/(/a$  | $S\rightarrow(\cdot S),)/+/*/(/a$   |                                   | $S\rightarrow S*\cdot,)/+/*/(/a$  | $S\rightarrow a\cdot,)/+/*/(/a$   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow a\cdot ,\$/+/*/(/a$                            |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow S*\cdot,\$/+/*/(/a$                            |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow a\cdot,)/+/*/(/a$                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow(S)\cdot,\$/+/*/(/a$                            |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow S*\cdot,)/+/*/(/a$                             |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
|                                                              |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |
| $S\rightarrow(S)\cdot,)/+/*/(/a$                             |                                                              |                                                              |                                     |                                     |                                   |                                   |                                   |

And the LALR items are
$$
S’\rightarrow \cdot S,\$\\\\
S'\rightarrow S\cdot,\$\\S\rightarrow S\cdot+S,\$/+/*/(/a\\S\rightarrow S\cdot S,\$/+/*/(/a\\S\rightarrow S\cdot *,\$/+/*/(/a\\\\
S\rightarrow (\cdot S),\$/+/*/(/)/a\\\\
S\rightarrow SS\cdot,\$/+/*/(/)/a\\S\rightarrow S\cdot+S,\$/+/*/(/)/a\\S\rightarrow S\cdot S,\$/+/*/(/)/a\\S\rightarrow S\cdot *,\$/+/*/(/)/a\\\\
S\rightarrow S+\cdot S,\$/+/*/(/)/a\\\\
S\rightarrow(S\cdot),\$/+/*/(/)/a\\S\rightarrow S\cdot+S,)/+/*/(/a\\S\rightarrow S\cdot S,)/+/*/(/a\\S\rightarrow S\cdot*,)/+/*/(/a\\\\
S\rightarrow S+S\cdot,\$/+/*/(/)/a\\S\rightarrow S\cdot+S,\$/+/*/(/)/a\\S\rightarrow S\cdot S,\$/+/*/(/)/a\\S\rightarrow S\cdot *,\$/+/*/(/)/a\\\\
S\rightarrow a\cdot ,\$/+/*/(/)/a\\\\
S\rightarrow S*\cdot,\$/+/*/(/)/a\\\\
S\rightarrow(S)\cdot,\$/+/*/(/)/a
$$

#### e

The augmented grammar is
$$
S'\rightarrow S\\
S\rightarrow(L)\;|\;a\\
L\rightarrow L,S\;|\;S
$$
First, construct the FIRST table

|      | FIRST     |
| ---- | --------- |
| $S$  | $\{(,a\}$ |
| $L$  | $\{(,a\}$ |

And then construct the LR table directly

| Kernel                                                 | Nonkernel                                                    | $S$                         | $L$                                                    | (                           | )                          | $a$                       | $,$                          |
| ------------------------------------------------------ | ------------------------------------------------------------ | --------------------------- | ------------------------------------------------------ | --------------------------- | -------------------------- | ------------------------- | ---------------------------- |
| $S'\rightarrow\cdot S,\$$                              | $S\rightarrow\cdot(L),\$\\S\rightarrow\cdot a,\$$            | $S'\rightarrow S\cdot,\$$   |                                                        | $S\rightarrow (\cdot L),\$$ |                            | $S\rightarrow a\cdot,\$$  |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $S\rightarrow (\cdot L),\$$                            | $L\rightarrow\cdot L,S,)/,\\L\rightarrow\cdot S,)/,\\S\rightarrow\cdot(L),)/,\\S\rightarrow\cdot a,)/,$ | $L\rightarrow S\cdot,)/,$   | $S\rightarrow (L\cdot),\$\\L\rightarrow L\cdot,S,)/,$  | $S\rightarrow(\cdot L),)/,$ |                            | $S\rightarrow a\cdot,)/,$ |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $S\rightarrow (L\cdot),\$\\L\rightarrow L\cdot,S,)/,$  |                                                              |                             |                                                        |                             | $S\rightarrow(L)\cdot,\$$  |                           | $L\rightarrow L,\cdot S,)/,$ |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $S\rightarrow(\cdot L),)/,$                            | $L\rightarrow\cdot L,S,)/,\\L\rightarrow\cdot S,)/,\\S\rightarrow\cdot(L),)/,\\S\rightarrow\cdot a,)/,$ | $L\rightarrow S\cdot,)/,$   | $S\rightarrow (L\cdot),)/,\\L\rightarrow L\cdot,S,)/,$ | $S\rightarrow(\cdot L),)/,$ |                            | $S\rightarrow a\cdot,)/,$ |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $L\rightarrow L,\cdot S,)/,$                           | $S\rightarrow\cdot(L),)/,\\S\rightarrow\cdot a,)/,$          | $L\rightarrow L,S\cdot,)/,$ |                                                        | $S\rightarrow(\cdot L),)/,$ |                            | $S\rightarrow a\cdot,)/,$ |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $S\rightarrow (L\cdot),)/,\\L\rightarrow L\cdot,S,)/,$ |                                                              |                             |                                                        |                             | $S\rightarrow(L)\cdot,)/,$ |                           | $L\rightarrow L,\cdot S,)/,$ |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $S'\rightarrow S\cdot,\$$                              |                                                              |                             |                                                        |                             |                            |                           |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $S\rightarrow a\cdot,\$$                               |                                                              |                             |                                                        |                             |                            |                           |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $L\rightarrow S\cdot,)/,$                              |                                                              |                             |                                                        |                             |                            |                           |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $S\rightarrow a\cdot,)/,$                              |                                                              |                             |                                                        |                             |                            |                           |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $S\rightarrow(L)\cdot,\$$                              |                                                              |                             |                                                        |                             |                            |                           |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $L\rightarrow L,S\cdot,)/,$                            |                                                              |                             |                                                        |                             |                            |                           |                              |
|                                                        |                                                              |                             |                                                        |                             |                            |                           |                              |
| $S\rightarrow(L)\cdot,)/,$                             |                                                              |                             |                                                        |                             |                            |                           |                              |

And the LALR items are
$$
S'\rightarrow\cdot S,\$\\\\
S\rightarrow(\cdot L),)/,/\$\\\\
S\rightarrow (L\cdot),)/,/\$\\L\rightarrow L\cdot,S,)/,\\\\
L\rightarrow L,\cdot S,)/,\\\\
S'\rightarrow S\cdot,\$\\\\
S\rightarrow a\cdot,)/,/\$\\\\
L\rightarrow S\cdot,)/,\\\\
S\rightarrow(L)\cdot,)/,/\$\\\\
L\rightarrow L,S\cdot,)/,
$$

#### f

The augmented grammar is
$$
S'\rightarrow S\\
S\rightarrow aSbS\;|\;bSaS\;|\;\epsilon
$$
First, construct the FIRST table

|      | FIRST              |
| ---- | ------------------ |
| $S$  | $\{a,b,\epsilon\}$ |

And then construct the LR table directly

| Kernel                       | Nonkernel                                                    | $S$                          | $a$                          | $b$                          |
| ---------------------------- | ------------------------------------------------------------ | ---------------------------- | ---------------------------- | ---------------------------- |
| $S'\rightarrow\cdot S,\$$    | $S\rightarrow\cdot aSbS,\$\\S\rightarrow\cdot bSaS,\$\\S\rightarrow\cdot,\$$ | $S'\rightarrow S\cdot,\$$    | $S\rightarrow a\cdot SbS,\$$ | $S\rightarrow b\cdot SaS,\$$ |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow a\cdot SbS,\$$ | $S\rightarrow\cdot aSbS,b\\S\rightarrow\cdot bSaS,b\\S\rightarrow\cdot,b$ | $S\rightarrow aS\cdot bS,\$$ | $S\rightarrow a\cdot SbS,b$  | $S\rightarrow b\cdot SaS,b$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow b\cdot SaS,\$$ | $S\rightarrow\cdot aSbS,a\\S\rightarrow\cdot bSaS,a\\S\rightarrow\cdot,a$ | $S\rightarrow bS\cdot aS,\$$ | $S\rightarrow a\cdot SbS,a$  | $S\rightarrow b\cdot SaS,a$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow aS\cdot bS,\$$ |                                                              |                              |                              | $S\rightarrow aSb\cdot S,\$$ |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow a\cdot SbS,b$  | $S\rightarrow\cdot aSbS,b\\S\rightarrow\cdot bSaS,b\\S\rightarrow\cdot,b$ | $S\rightarrow aS\cdot bS,b$  | $S\rightarrow a\cdot SbS,b$  | $S\rightarrow b\cdot SaS,b$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow b\cdot SaS,b$  | $S\rightarrow\cdot aSbS,a\\S\rightarrow\cdot bSaS,a\\S\rightarrow\cdot,a$ | $S\rightarrow bS\cdot aS,b$  | $S\rightarrow a\cdot SbS,a$  | $S\rightarrow b\cdot SaS,a$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow bS\cdot aS,\$$ |                                                              |                              | $S\rightarrow bSa\cdot S,\$$ |                              |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow a\cdot SbS,a$  | $S\rightarrow\cdot aSbS,b\\S\rightarrow\cdot bSaS,b\\S\rightarrow\cdot,b$ | $S\rightarrow aS\cdot bS,a$  | $S\rightarrow a\cdot SbS,b$  | $S\rightarrow b\cdot SaS,b$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow b\cdot SaS,a$  | $S\rightarrow\cdot aSbS,a\\S\rightarrow\cdot bSaS,a\\S\rightarrow\cdot,a$ | $S\rightarrow bS\cdot aS,a$  | $S\rightarrow a\cdot SbS,a$  | $S\rightarrow b\cdot SaS,a$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow aSb\cdot S,\$$ | $S\rightarrow\cdot aSbS,\$\\S\rightarrow\cdot bSaS,\$\\S\rightarrow\cdot,\$$ | $S\rightarrow aSbS\cdot,\$$  | $S\rightarrow a\cdot SbS,\$$ | $S\rightarrow b\cdot SaS,\$$ |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow aS\cdot bS,b$  |                                                              |                              |                              | $S\rightarrow aSb\cdot S,b$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow bS\cdot aS,b$  |                                                              |                              | $S\rightarrow bSa\cdot S,b$  |                              |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow bSa\cdot S,\$$ | $S\rightarrow\cdot aSbS,\$\\S\rightarrow\cdot bSaS,\$\\S\rightarrow\cdot,\$$ | $S\rightarrow bSaS\cdot,\$$  | $S\rightarrow a\cdot SbS,\$$ | $S\rightarrow b\cdot SaS,\$$ |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow aS\cdot bS,a$  |                                                              |                              |                              | $S\rightarrow aSb\cdot S,a$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow bS\cdot aS,a$  |                                                              |                              | $S\rightarrow bSa\cdot S,a$  |                              |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow aSb\cdot S,b$  | $S\rightarrow\cdot aSbS,b\\S\rightarrow\cdot bSaS,b\\S\rightarrow\cdot,b$ | $S\rightarrow aSbS\cdot,b$   | $S\rightarrow a\cdot SbS,b$  | $S\rightarrow b\cdot SaS,b$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow bSa\cdot S,b$  | $S\rightarrow\cdot aSbS,b\\S\rightarrow\cdot bSaS,b\\S\rightarrow\cdot,b$ | $S\rightarrow bSaS\cdot,b$   | $S\rightarrow a\cdot SbS,b$  | $S\rightarrow b\cdot SaS,b$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow aSb\cdot S,a$  | $S\rightarrow\cdot aSbS,a\\S\rightarrow\cdot bSaS,a\\S\rightarrow\cdot,a$ | $S\rightarrow aSbS\cdot,a$   | $S\rightarrow a\cdot SbS,a$  | $S\rightarrow b\cdot SaS,a$  |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow bSa\cdot S,a$  | $S\rightarrow\cdot aSbS,a\\S\rightarrow\cdot bSaS,a\\S\rightarrow\cdot,a$ | $S\rightarrow bSaS\cdot,a$   | $S\rightarrow a\cdot SbS,a$  | $S\rightarrow b\cdot SaS,a$  |
|                              |                                                              |                              |                              |                              |
| $S'\rightarrow S\cdot,\$$    |                                                              |                              |                              |                              |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow aSbS\cdot,\$$  |                                                              |                              |                              |                              |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow bSaS\cdot,\$$  |                                                              |                              |                              |                              |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow aSbS\cdot,b$   |                                                              |                              |                              |                              |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow bSaS\cdot,b$   |                                                              |                              |                              |                              |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow aSbS\cdot,a$   |                                                              |                              |                              |                              |
|                              |                                                              |                              |                              |                              |
| $S\rightarrow bSaS\cdot,a$   |                                                              |                              |                              |                              |

And the LALR items are
$$
S'\rightarrow\cdot S,\$\\\\
S\rightarrow a\cdot SbS,a/b/\$\\\\
S\rightarrow b\cdot SaS,a/b/\$\\\\
S\rightarrow aS\cdot bS,a/b/\$\\\\
S\rightarrow bS\cdot aS,a/b/\$\\\\
S\rightarrow aSb\cdot S,a/b/\$\\\\
S\rightarrow bSa\cdot S,a/b/\$\\\\
S'\rightarrow S\cdot,\$\\\\
S\rightarrow aSbS\cdot,a/b/\$\\\\
S\rightarrow bSaS\cdot,a/b/\$\\\\
$$

#### g

The augmented grammar is
$$
S'\rightarrow bexpr\\
bexpr\rightarrow bexpr\textbf{ or }bterm\;|\;bterm\\
bterm\rightarrow bterm\textbf{ and }bfactor\;|\;bfactor\\
bfactor\rightarrow\textbf{not }bfactor\;|\;(bexpr)\;|\;\textbf{true}\;|\;\textbf{false}
$$
And then construct the LR table directly

| Kernel                                                       | Nonkernel                                                    | $bexpr$                                                      | $bterm$                                                      | $bfactor$                                                    | or                                                           | and                                                          | not                                                          | (                                                            | )                                                            | true                                                         | false                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| $S’\rightarrow\cdot bexpr,\$$                                | $bexpr\rightarrow\cdot bexpr\textbf{ or }bterm,\textbf{or}/\$\\bexpr\rightarrow\cdot bterm,\textbf{or}/\$\\bterm\rightarrow\cdot bterm\textbf{ and }bfactor,\textbf{or}/\textbf{and}/\$\\bterm\rightarrow\cdot bfactor,\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{not }bfactor,\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot(bexpr),\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{true},\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{false},\textbf{or}/\textbf{and}/\$$ | $S’\rightarrow bexpr\cdot,\$\\bexpr\rightarrow bexpr\cdot\textbf{or }bterm,\textbf{or}/\$$ | $bexpr\rightarrow bterm\cdot,\textbf{or}/\$\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/\$$ | $bterm\rightarrow bfactor\cdot,\textbf{or}/\textbf{and}/\$$  |                                                              |                                                              | $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/\$$ |                                                              | $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/\$$ |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $S’\rightarrow bexpr\cdot,\$\\bexpr\rightarrow bexpr\cdot\textbf{or }bterm,\textbf{or}/\$$ |                                                              |                                                              |                                                              |                                                              | $bexpr\rightarrow bexpr\textbf{ or}\cdot bterm,\textbf{or}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bexpr\rightarrow bterm\cdot,\textbf{or}/\$\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              | $bterm\rightarrow bterm\textbf{ and}\cdot bfactor,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow\cdot\textbf{not }bfactor,\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot(bexpr),\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{true},\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{false},\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              | $bfactor\rightarrow\textbf{not } bfactor\cdot,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              | $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/\$$ |                                                              | $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/\$$ |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/\$$ | $bexpr\rightarrow\cdot bexpr\textbf{ or }bterm,\textbf{or}/)\\bexpr\rightarrow\cdot bterm,\textbf{or}/)\\bterm\rightarrow\cdot bterm\textbf{ and }bfactor,\textbf{or}/\textbf{and}/)\\bterm\rightarrow\cdot bfactor,\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{not }bfactor,\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot(bexpr),\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{true},\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{false},\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow( bexpr\cdot),\textbf{or}/\textbf{and}/\$\\bexpr\rightarrow bexpr\cdot\textbf{or }bterm,\textbf{or}/)$ | $bexpr\rightarrow bterm\cdot,\textbf{or}/)\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/)$ | $bterm\rightarrow bfactor\cdot,\textbf{or}/\textbf{and}/)$   |                                                              |                                                              | $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/)$ |                                                              | $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/)$ |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bexpr\rightarrow bexpr\textbf{ or}\cdot bterm,\textbf{or}/\$$ | $bterm\rightarrow\cdot bterm\textbf{ and }bfactor,\textbf{or}/\textbf{and}/\$\\bterm\rightarrow\cdot bfactor,\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{not }bfactor,\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot(bexpr),\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{true},\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{false},\textbf{or}/\textbf{and}/\$$ |                                                              | $bexpr\rightarrow bexpr\textbf{ or } bterm\cdot,\textbf{or}/\$\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/\$$ | $bterm\rightarrow bfactor\cdot,\textbf{or}/\textbf{and}/\$$  |                                                              |                                                              | $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/\$$ |                                                              | $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/\$$ |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bterm\rightarrow bterm\textbf{ and}\cdot bfactor,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow\cdot\textbf{not }bfactor,\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot(bexpr),\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{true},\textbf{or}/\textbf{and}/\$\\bfactor\rightarrow\cdot\textbf{false},\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              | $bterm\rightarrow bterm\textbf{ and }bfactor\cdot,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              | $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/\$$ |                                                              | $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/\$$ | $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/\$$ |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow( bexpr\cdot),\textbf{or}/\textbf{and}/\$\\bexpr\rightarrow bexpr\cdot\textbf{or }bterm,\textbf{or}/)$ |                                                              |                                                              |                                                              |                                                              | $bexpr\rightarrow bexpr\textbf{ or}\cdot bterm,\textbf{or}/)$ |                                                              |                                                              |                                                              | $bfactor\rightarrow( bexpr)\cdot,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bexpr\rightarrow bterm\cdot,\textbf{or}/)\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |                                                              |                                                              |                                                              | $bterm\rightarrow bterm\textbf{ and}\cdot bfactor,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow\cdot\textbf{not }bfactor,\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot(bexpr),\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{true},\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{false},\textbf{or}/\textbf{and}/)$ |                                                              |                                                              | $bfactor\rightarrow\textbf{not } bfactor\cdot,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              | $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/)$ |                                                              | $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/)$ |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/)$ | $bexpr\rightarrow\cdot bexpr\textbf{ or }bterm,\textbf{or}/)\\bexpr\rightarrow\cdot bterm,\textbf{or}/)\\bterm\rightarrow\cdot bterm\textbf{ and }bfactor,\textbf{or}/\textbf{and}/)\\bterm\rightarrow\cdot bfactor,\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{not }bfactor,\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot(bexpr),\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{true},\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{false},\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow( bexpr\cdot),\textbf{or}/\textbf{and}/)\\bexpr\rightarrow bexpr\cdot\textbf{or }bterm,\textbf{or}/)$ | $bexpr\rightarrow bterm\cdot,\textbf{or}/)\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/)$ | $bterm\rightarrow bfactor\cdot,\textbf{or}/\textbf{and}/)$   |                                                              |                                                              | $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/)$ |                                                              | $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/)$ |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bexpr\rightarrow bexpr\textbf{ or } bterm\cdot,\textbf{or}/\$\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              | $bterm\rightarrow bterm\textbf{ and}\cdot bfactor,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bexpr\rightarrow bexpr\textbf{ or}\cdot bterm,\textbf{or}/)$ | $bterm\rightarrow\cdot bterm\textbf{ and }bfactor,\textbf{or}/\textbf{and}/)\\bterm\rightarrow\cdot bfactor,\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{not }bfactor,\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot(bexpr),\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{true},\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{false},\textbf{or}/\textbf{and}/)$ |                                                              | $bexpr\rightarrow bexpr\textbf{ or } bterm\cdot,\textbf{or}/)\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/)$ | $bterm\rightarrow bfactor\cdot,\textbf{or}/\textbf{and}/)$   |                                                              |                                                              | $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/)$ |                                                              | $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/)$ |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bterm\rightarrow bterm\textbf{ and}\cdot bfactor,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow\cdot\textbf{not }bfactor,\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot(bexpr),\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{true},\textbf{or}/\textbf{and}/)\\bfactor\rightarrow\cdot\textbf{false},\textbf{or}/\textbf{and}/)$ |                                                              |                                                              | $bterm\rightarrow bterm\textbf{ and }bfactor\cdot,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              | $bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/)$ |                                                              | $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/)$ | $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/)$ |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow( bexpr\cdot),\textbf{or}/\textbf{and}/)\\bexpr\rightarrow bexpr\cdot\textbf{or }bterm,\textbf{or}/)$ |                                                              |                                                              |                                                              |                                                              | $bexpr\rightarrow bexpr\textbf{ or}\cdot bterm,\textbf{or}/)$ |                                                              |                                                              |                                                              | $bfactor\rightarrow( bexpr)\cdot,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bexpr\rightarrow bexpr\textbf{ or } bterm\cdot,\textbf{or}/)\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |                                                              |                                                              |                                                              | $bterm\rightarrow bterm\textbf{ and}\cdot bfactor,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bterm\rightarrow bfactor\cdot,\textbf{or}/\textbf{and}/\$$  |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow\textbf{not } bfactor\cdot,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bterm\rightarrow bfactor\cdot,\textbf{or}/\textbf{and}/)$   |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bterm\rightarrow bterm\textbf{ and }bfactor\cdot,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow( bexpr)\cdot,\textbf{or}/\textbf{and}/\$$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow\textbf{not } bfactor\cdot,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bterm\rightarrow bterm\textbf{ and }bfactor\cdot,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
| $bfactor\rightarrow( bexpr)\cdot,\textbf{or}/\textbf{and}/)$ |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |

And the LALR items are
$$
S’\rightarrow\cdot bexpr,\$\\\\
S’\rightarrow bexpr\cdot,\$\\bexpr\rightarrow bexpr\cdot\textbf{or }bterm,\textbf{or}/\$\\\\
bexpr\rightarrow bterm\cdot,\textbf{or}/)/\$\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/)/\$\\\\
bfactor\rightarrow\textbf{not}\cdot bfactor,\textbf{or}/\textbf{and}/)/\$\\\\
bfactor\rightarrow(\cdot bexpr),\textbf{or}/\textbf{and}/)/\$\\\\
bexpr\rightarrow bexpr\textbf{ or}\cdot bterm,\textbf{or}/)/\$\\\\
bterm\rightarrow bterm\textbf{ and}\cdot bfactor,\textbf{or}/\textbf{and}/)/\$\\\\
bfactor\rightarrow( bexpr\cdot),\textbf{or}/\textbf{and}/)/\$\\bexpr\rightarrow bexpr\cdot\textbf{or }bterm,\textbf{or}/)\\\\
bexpr\rightarrow bexpr\textbf{ or } bterm\cdot,\textbf{or}/)/\$\\bterm\rightarrow bterm\cdot\textbf{and }bfactor,\textbf{or}/\textbf{and}/)/\$\\\\
bterm\rightarrow bfactor\cdot,\textbf{or}/\textbf{and}/)/\$\\\\
bfactor\rightarrow\textbf{true}\cdot,\textbf{or}/\textbf{and}/)/\$\\\\
bfactor\rightarrow\textbf{false}\cdot,\textbf{or}/\textbf{and}/)/\$\\\\
bfactor\rightarrow\textbf{not } bfactor\cdot,\textbf{or}/)/\textbf{and}/\$\\\\
bterm\rightarrow bterm\textbf{ and }bfactor\cdot,\textbf{or}/\textbf{and}/)/\$\\\\
bfactor\rightarrow( bexpr)\cdot,\textbf{or}/\textbf{and}/)/\$\\\\
$$

## Problem 3

### Problem Description

For the grammar of Exercise 4.7.1, use Algorithm 4.63 to compute the collection of LALR sets of items from the kernels of the LR(0) sets of items.

### Solution

First build the parsing table:

|       | Kernel                                                       | Nonkernel                                                    | $S$                                                          | $+$                     | $*$                     | $a$                   |
| ----- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------- | ----------------------- | --------------------- |
| $I_0$ | $S’\rightarrow\cdot S$                                       | $S\rightarrow\cdot SS+\\S\rightarrow\cdot SS*\\S\rightarrow\cdot a$ | $S'\rightarrow S\cdot\\S\rightarrow S\cdot S+\\S\rightarrow S\cdot S*$ |                         |                         | $S\rightarrow a\cdot$ |
|       |                                                              |                                                              |                                                              |                         |                         |                       |
| $I_1$ | $S'\rightarrow S\cdot\\S\rightarrow S\cdot S+\\S\rightarrow S\cdot S*$ | $S\rightarrow\cdot SS+\\S\rightarrow\cdot SS*\\S\rightarrow\cdot a$ | $S\rightarrow SS\cdot+\\S\rightarrow SS\cdot*\\S\rightarrow S\cdot S+\\S\rightarrow S\cdot S*$ |                         |                         | $S\rightarrow a\cdot$ |
|       |                                                              |                                                              |                                                              |                         |                         |                       |
| $I_2$ | $S\rightarrow SS\cdot+\\S\rightarrow SS\cdot*\\S\rightarrow S\cdot S+\\S\rightarrow S\cdot S*$ | $S\rightarrow\cdot SS+\\S\rightarrow\cdot SS*\\S\rightarrow\cdot a$ | $S\rightarrow SS\cdot+\\S\rightarrow SS\cdot*\\S\rightarrow S\cdot S+\\S\rightarrow S\cdot S*$ | $S\rightarrow SS+\cdot$ | $S\rightarrow SS*\cdot$ | $S\rightarrow a\cdot$ |
|       |                                                              |                                                              |                                                              |                         |                         |                       |
| $I_3$ | $S\rightarrow a\cdot$                                        |                                                              |                                                              |                         |                         |                       |
|       |                                                              |                                                              |                                                              |                         |                         |                       |
| $I_4$ | $S\rightarrow SS+\cdot$                                      |                                                              |                                                              |                         |                         |                       |
|       |                                                              |                                                              |                                                              |                         |                         |                       |
| $I_5$ | $S\rightarrow SS*\cdot$                                      |                                                              |                                                              |                         |                         |                       |

#### $I_0$ Analysis

Consider
$$
I_0:S'\rightarrow\cdot S,\#
$$
which could be expanded as
$$
S'\rightarrow\cdot S,\#\\
S\rightarrow\cdot SS+,\#/a\\
S\rightarrow\cdot SS*,\#/a\\
S\rightarrow\cdot a,\#/a
$$
Which further generates
$$
I_1:S'\rightarrow S\cdot,\#\\
I_1:S\rightarrow S\cdot S+,\#/a\\
I_1:S\rightarrow S\cdot S*,\#/a\\
I_3:S\rightarrow a\cdot,\#/a
$$

#### $I_1$ Analysis

Consider
$$
I_1:S\rightarrow S\cdot S+,\#
$$
which could be expanded as
$$
S\rightarrow S\cdot S+,\#\\
S\rightarrow\cdot SS+,+/a\\
S\rightarrow\cdot SS*,+/a\\
S\rightarrow\cdot a,+/a
$$
Which further generates
$$
I_2:S\rightarrow SS\cdot +,\#\\
I_2:S\rightarrow S\cdot S+,+/a\\
I_2:S\rightarrow S\cdot S*,+/a\\
I_3:S\rightarrow a\cdot,+/a
$$
Consider
$$
I_1:S\rightarrow S\cdot S*,\#
$$
which could be expanded as
$$
S\rightarrow S\cdot S*,\#\\
S\rightarrow\cdot SS+,*/a\\
S\rightarrow\cdot SS*,*/a\\
S\rightarrow \cdot a,*/a
$$
Which further generates
$$
I_2:S\rightarrow SS\cdot*,\#\\
I_2:S\rightarrow S\cdot S+,*/a\\
I_2:S\rightarrow S\cdot S*,*/a\\
I_3:S\rightarrow a\cdot,*/a
$$

#### $I_2$ Analysis

Consider
$$
I_2:S\rightarrow SS\cdot+,\#
$$
It simply generates
$$
I_4:S\rightarrow SS+\cdot,\#
$$
Consider
$$
I_2:S\rightarrow SS\cdot*,\#
$$
It simply generates
$$
I_5:S\rightarrow SS*\cdot,\#
$$
Consider
$$
I_2:S\rightarrow S\cdot S+,\#
$$
which could be expanded as
$$
S\rightarrow S\cdot S+,\#\\
S\rightarrow\cdot SS+,+/a\\
S\rightarrow\cdot SS*,+/a\\
S\rightarrow\cdot a,+/a
$$
Which further generates
$$
I_2:S\rightarrow SS\cdot +,\#\\
I_2:S\rightarrow S\cdot S+,+/a\\
I_2:S\rightarrow S\cdot S*,+/a\\
I_3:S\rightarrow a\cdot,+/a
$$
Consider
$$
I_2:S\rightarrow S\cdot S*,\#
$$
which could be expanded as
$$
S\rightarrow S\cdot S*,\#\\
S\rightarrow\cdot SS+,*/a\\
S\rightarrow\cdot SS*,*/a\\
S\rightarrow \cdot a,*/a
$$
Which further generates
$$
I_2:S\rightarrow SS\cdot*,\#\\
I_2:S\rightarrow S\cdot S+,*/a\\
I_2:S\rightarrow S\cdot S*,*/a\\
I_3:S\rightarrow \cdot a,*/a
$$

#### Propagate Table

|       | Kernel                   | To                           |
| ----- | ------------------------ | ---------------------------- |
| $I_0$ | $S’\rightarrow\cdot S$   | $I_1:S'\rightarrow S\cdot$   |
|       |                          | $I_1:S\rightarrow S\cdot S+$ |
|       |                          | $I_1:S\rightarrow S\cdot S*$ |
|       |                          | $I_3:S\rightarrow a\cdot$    |
| $I_1$ | $S\rightarrow S\cdot S+$ | $I_2:S\rightarrow SS\cdot+$  |
|       | $S\rightarrow S\cdot S*$ | $I_2:S\rightarrow SS\cdot *$ |
| $I_2$ | $S\rightarrow SS\cdot+$  | $I_4:S\rightarrow SS+\cdot$  |
|       | $S\rightarrow SS\cdot *$ | $I_5:S\rightarrow SS*\cdot$  |
|       | $S\rightarrow S\cdot S+$ | $I_2:S\rightarrow SS\cdot +$ |
|       | $S\rightarrow S\cdot S*$ | $I_2:S\rightarrow SS\cdot*$  |

#### Pass

| Set   | Item                     | Pass 0  | Pass 1     | Pass 2     | Pass 3     |
| ----- | ------------------------ | ------- | ---------- | ---------- | ---------- |
| $I_0$ | $S’\rightarrow\cdot S$   | \$      | $\$$       | $\$$       | $\$$       |
| $I_1$ | $S'\rightarrow S\cdot$   |         | $\$$       | $\$$       | $\$$       |
|       | $S\rightarrow S\cdot S+$ | $a$     | $a/\$$     | $a/\$$     | $a/\$$     |
|       | $S\rightarrow S\cdot S*$ | $a$     | $a/\$$     | $a/\$$     | $a/\$$     |
| $I_2$ | $S\rightarrow SS\cdot+$  |         | $+/*/a$    | $+/*/a/\$$ | $+/*/a/\$$ |
|       | $S\rightarrow SS\cdot*$  |         | $+/*/a$    | $+/*/a/\$$ | $+/*/a/\$$ |
|       | $S\rightarrow S\cdot S+$ | $+/*/a$ | $+/*/a$    | $+/*/a$    | $+/*/a$    |
|       | $S\rightarrow S\cdot S*$ | $+/*/a$ | $+/*/a$    | $+/*/a$    | $+/*/a$    |
| $I_3$ | $S\rightarrow a\cdot$    | $+/*/a$ | $+/*/a/\$$ | $+/*/a/\$$ | $+/*/a/\$$ |
| $I_4$ | $S\rightarrow SS+\cdot$  |         |            | $+/*/a$    | $+/*/a/\$$ |
| $I_5$ | $S\rightarrow SS*\cdot$  |         |            | $+/*/a$    | $+/*/a/\$$ |

We can derive those items directly by the table:
$$
S'\rightarrow\cdot S,\$\\\\S’\rightarrow S\cdot,\$\\S\rightarrow S\cdot S+,a/\$\\S\rightarrow S\cdot S*,a/\$\\\\S\rightarrow SS\cdot +,+/*/a/\$\\S\rightarrow SS\cdot *,+/*/a/\$\\S\rightarrow S\cdot S+,+/*/a\\S\rightarrow S\cdot S*,+/*/a\\\\S\rightarrow a\cdot,+/*/a/\$\\\\S\rightarrow SS+\cdot,+/*/a/\$\\\\S\rightarrow SS*\cdot,+/*/a/\$
$$

## Problem 4

### Problem Description

Show that the following grammar
$$
S\rightarrow Aa\;|\;bAc\;|\;dc\;|\;bda\\
A\rightarrow d
$$
is LALR(1) but not SLR(1).

### Solution

The augmented grammar is
$$
S'\rightarrow S\\
S\rightarrow Aa\;|\;bAc\;|\;dc\;|\;bda\\
A\rightarrow d
$$
The LR(1) table is

| Kernel                                                 | Nonkernel                                                    | $S$                       | $A$                         | $a$                          | $b$                                                    | $c$                        | $d$                                                |
| ------------------------------------------------------ | ------------------------------------------------------------ | ------------------------- | --------------------------- | ---------------------------- | ------------------------------------------------------ | -------------------------- | -------------------------------------------------- |
| $S'\rightarrow\cdot S,\$$                              | $S\rightarrow\cdot Aa,\$\\S\rightarrow\cdot bAc,\$\\S\rightarrow\cdot dc,\$\\S\rightarrow\cdot bda,\$\\A\rightarrow\cdot d,a$ | $S'\rightarrow S\cdot,\$$ | $S\rightarrow A\cdot a,\$$  |                              | $S\rightarrow b\cdot Ac,\$\\S\rightarrow b\cdot da,\$$ |                            | $S\rightarrow d\cdot c,\$\\A\rightarrow d\cdot,a$  |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S\rightarrow A\cdot a,\$$                             |                                                              |                           |                             | $S\rightarrow Aa\cdot,\$$    |                                                        |                            |                                                    |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S\rightarrow b\cdot Ac,\$\\S\rightarrow b\cdot da,\$$ | $A\rightarrow\cdot d,c$                                      |                           | $S\rightarrow bA\cdot c,\$$ |                              |                                                        |                            | $S\rightarrow bd\cdot a,\$\\A\rightarrow d\cdot,c$ |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S\rightarrow d\cdot c,\$\\A\rightarrow d\cdot,a$      |                                                              |                           |                             |                              |                                                        | $S\rightarrow dc\cdot,\$$  |                                                    |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S\rightarrow bA\cdot c,\$$                            |                                                              |                           |                             |                              |                                                        | $S\rightarrow bAc\cdot,\$$ |                                                    |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S\rightarrow bd\cdot a,\$\\A\rightarrow d\cdot,c$     |                                                              |                           |                             | $S\rightarrow bda\cdot \,\$$ |                                                        |                            |                                                    |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S'\rightarrow S\cdot,\$$                              |                                                              |                           |                             |                              |                                                        |                            |                                                    |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S\rightarrow Aa\cdot,\$$                              |                                                              |                           |                             |                              |                                                        |                            |                                                    |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S\rightarrow dc\cdot,\$$                              |                                                              |                           |                             |                              |                                                        |                            |                                                    |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S\rightarrow bAc\cdot,\$$                             |                                                              |                           |                             |                              |                                                        |                            |                                                    |
|                                                        |                                                              |                           |                             |                              |                                                        |                            |                                                    |
| $S\rightarrow bda\cdot \,\$$                           |                                                              |                           |                             |                              |                                                        |                            |                                                    |

This table already contains all the LALR items, and it is the same as LR(0) if remove the lookahead symbol. Then rewrite the table

| Set      | $S$   | $A$   | $a$      | $b$   | $c$   | $d$   |
| -------- | ----- | ----- | -------- | ----- | ----- | ----- |
| $S_0$    | $S_6$ | $S_1$ |          | $S_2$ |       | $S_3$ |
| $S_1$    |       |       | $S_7$    |       |       |       |
| $S_2$    |       | $S_4$ |          |       |       | $S_5$ |
| $S_3$    |       |       |          |       | $S_8$ |       |
| $S_4$    |       |       |          |       | $S_9$ |       |
| $S_5$    |       |       | $S_{10}$ |       |       |       |
| $S_6$    |       |       |          |       |       |       |
| $S_7$    |       |       |          |       |       |       |
| $S_8$    |       |       |          |       |       |       |
| $S_9$    |       |       |          |       |       |       |
| $S_{10}$ |       |       |          |       |       |       |

The initial GOTO table is

| Set      | $a$      | $b$   | $c$   | $d$   |
| -------- | -------- | ----- | ----- | ----- |
| $S_0$    |          | s2 |       | s3 |
| $S_1$    | s7    |       |       |       |
| $S_2$    |          |       |       | s5 |
| $S_3$    |          |       | s8 |       |
| $S_4$    |          |       | s9 |       |
| $S_5$    | s10 |       |       |       |
| $S_6$    |          |       |       |       |
| $S_7$    |          |       |       |       |
| $S_8$    |          |       |       |       |
| $S_9$    |          |       |       |       |
| $S_{10}$ |          |       |       |       |

Let r1 represents $A\rightarrow d\cdot$, r2 represents $S\rightarrow Aa\cdot$, r3 represents $S\rightarrow dc\cdot$, r4 represents $S\rightarrow bAc\cdot$ and r5 represents $S\rightarrow bda\cdot$.

Consider the FIRST table

|      | FIRST     |
| ---- | --------- |
| $S$  | $\{b,d\}$ |
| $A$  | $\{d\}$   |

and the FOLLOW table:

|      | FOLLOW    |
| ---- | --------- |
| $S$  | $\{\$\}$  |
| $A$  | $\{a,c\}$ |

Then the final GOTO table is

| Set      | $a$      | $b$   | $c$   | $d$   | $\$$ |
| -------- | -------- | ----- | ----- | ----- | ----- |
| $S_0$    |          | s2 |       | s3 |  |
| $S_1$    | s7    |       |       |       |       |
| $S_2$    |          |       |       | s5 |  |
| $S_3$    | r1 |       | s8 |       |       |
|  | | | r1 |  |  |
| $S_4$    |          |       | s9 |       |       |
| $S_5$    | s10 |       | r1 |       |       |
|  | r1 | | | | |
| $S_6$    |          |       |       |       | accpet |
| $S_7$    |          |       |       |       | r2 |
| $S_8$    |          |       |       |       | r3 |
| $S_9$    |          |       |       |       | r4 |
| $S_{10}$ |          |       |       |       | r5 |

Since there’s more than one element in one entry, this language is not SLR(1). However, using the LALR(1) table, we can construct

| Set      | $a$      | $b$   | $c$   | $d$   | $\$$ |
| -------- | -------- | ----- | ----- | ----- | ----- |
| $S_0$    |          | s2 |       | s3 |  |
| $S_1$    | s7    |       |       |       |       |
| $S_2$    |          |       |       | s5 |  |
| $S_3$    | r1 |       | s8 |       |       |
| $S_4$    |          |       | s9 |       |       |
| $S_5$    | s10 |       | r1 |       |       |
| $S_6$    |          |       |       |       | accpet |
| $S_7$    |          |       |       |       | r2 |
| $S_8$    |          |       |       |       | r3 |
| $S_9$    |          |       |       |       | r4 |
| $S_{10}$ |          |       |       |       | r5 |

So this grammar is LALR(1).

## Problem 5

### Problem Description

Show that the following grammar
$$
S\rightarrow Aa\;|\;bAc\;|\;Bc\;|\;bBa\\
A\rightarrow d\\
B\rightarrow d
$$

### Solution

The augmented grammar is
$$
S'\rightarrow S\\
S\rightarrow Aa\;|\;bAc\;|\;Bc\;|\;bBa\\
A\rightarrow d\\
B\rightarrow d
$$
The LR(1) table is

| Kernel                                                 | Nonkernel                                                    | $S$                       | $A$                         | $B$                         | $a$                        | $b$                                                    | $c$                        | $d$                                            |
| ------------------------------------------------------ | ------------------------------------------------------------ | ------------------------- | --------------------------- | --------------------------- | -------------------------- | ------------------------------------------------------ | -------------------------- | ---------------------------------------------- |
| $S'\rightarrow \cdot S,\$$                             | $S\rightarrow\cdot Aa,\$\\S\rightarrow\cdot bAc,\$\\S\rightarrow\cdot Bc,\$\\S\rightarrow\cdot bBa,\$\\A\rightarrow\cdot d,a\\B\rightarrow\cdot d,c$ | $S’\rightarrow S\cdot,\$$ | $S\rightarrow A\cdot a,\$$  | $S\rightarrow B\cdot c,\$$  |                            | $S\rightarrow b\cdot Ac,\$\\S\rightarrow b\cdot Ba,\$$ |                            | $A\rightarrow d\cdot,a\\B\rightarrow d\cdot,c$ |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S\rightarrow A\cdot a,\$$                             |                                                              |                           |                             |                             | $S\rightarrow Aa\cdot,\$$  |                                                        |                            |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S\rightarrow B\cdot c,\$$                             |                                                              |                           |                             |                             |                            |                                                        | $S\rightarrow Bc\cdot,\$$  |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S\rightarrow b\cdot Ac,\$\\S\rightarrow b\cdot Ba,\$$ | $A\rightarrow \cdot d,c\\B\rightarrow \cdot d,a$             |                           | $S\rightarrow bA\cdot c,\$$ | $S\rightarrow bB\cdot a,\$$ |                            |                                                        |                            | $A\rightarrow d\cdot,c\\B\rightarrow d\cdot,a$ |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S\rightarrow bA\cdot c,\$$                            |                                                              |                           |                             |                             |                            |                                                        | $S\rightarrow bAc\cdot,\$$ |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S\rightarrow bB\cdot a,\$$                            |                                                              |                           |                             |                             | $S\rightarrow bBa\cdot,\$$ |                                                        |                            |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S’\rightarrow S\cdot,\$$                              |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $A\rightarrow d\cdot,a\\B\rightarrow d\cdot,c$         |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S\rightarrow Aa\cdot,\$$                              |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S\rightarrow Bc\cdot,\$$                              |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $A\rightarrow d\cdot,c\\B\rightarrow d\cdot,a$         |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S\rightarrow bAc\cdot,\$$                             |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
|                                                        |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |
| $S\rightarrow bBa\cdot,\$$                             |                                                              |                           |                             |                             |                            |                                                        |                            |                                                |

We can write the GOTO table as

|          | $a$  | $b$  | $c$  | $d$  | $\$$   |
| -------- | ---- | ---- | ---- | ---- | ------ |
| $S_0$    |      | s3   |      | s7   |        |
| $S_1$    | s8   |      |      |      |        |
| $S_2$    |      |      | s9   |      |        |
| $S_3$    |      |      |      | s10  |        |
| $S_4$    |      |      | s11  |      |        |
| $S_5$    | s12  |      |      |      |        |
| $S_6$    |      |      |      |      | accept |
| $S_7$    |      |      |      |      |        |
| $S_8$    |      |      |      |      |        |
| $S_9$    |      |      |      |      |        |
| $S_{10}$ |      |      |      |      |        |
| $S_{11}$ |      |      |      |      |        |
| $S_{12}$ |      |      |      |      |        |

Let r1 represents $A\rightarrow d\cdot$, r2 represents $B\rightarrow d\cdot$, r3 represents $S\rightarrow Aa\cdot$, r4 represents $S\rightarrow Bc\cdot$, r5 represents $S\rightarrow bAc\cdot$ and r6 represents $S\rightarrow bBa\cdot$. Then the table becomes

|          | $a$  | $b$  | $c$  | $d$  | $\$$   |
| -------- | ---- | ---- | ---- | ---- | ------ |
| $S_0$    |      | s3   |      | s7   |        |
| $S_1$    | s8   |      |      |      |        |
| $S_2$    |      |      | s9   |      |        |
| $S_3$    |      |      |      | s10  |        |
| $S_4$    |      |      | s11  |      |        |
| $S_5$    | s12  |      |      |      |        |
| $S_6$    |      |      |      |      | accept |
| $S_7$    | r1   |      | r2   |      |        |
| $S_8$    |      |      |      |      | r3     |
| $S_9$    |      |      |      |      | r4     |
| $S_{10}$ | r2   |      | r1   |      |        |
| $S_{11}$ |      |      |      |      | r5     |
| $S_{12}$ |      |      |      |      | r6     |

Thus this is a LR(1) grammar. To construct a LALR(1) item set we need to merge $S_7$ and $S_{10}$ into $S_{710}$

|           | $a$  | $b$  | $c$  | $d$  | $\$$   |
| --------- | ---- | ---- | ---- | ---- | ------ |
| $S_0$     |      | s3   |      | s710 |        |
| $S_1$     | s8   |      |      |      |        |
| $S_2$     |      |      | s9   |      |        |
| $S_3$     |      |      |      | s710 |        |
| $S_4$     |      |      | s11  |      |        |
| $S_5$     | s12  |      |      |      |        |
| $S_6$     |      |      |      |      | accept |
| $S_{710}$ |      |      |      |      |        |
| $S_8$     |      |      |      |      |        |
| $S_9$     |      |      |      |      |        |
| $S_{11}$  |      |      |      |      |        |
| $S_{12}$  |      |      |      |      |        |

Do the similar for the above table, and we get

|           | $a$  | $b$  | $c$  | $d$  | $\$$   |
| --------- | ---- | ---- | ---- | ---- | ------ |
| $S_0$     |      | s3   |      | s710 |        |
| $S_1$     | s8   |      |      |      |        |
| $S_2$     |      |      | s9   |      |        |
| $S_3$     |      |      |      | s710 |        |
| $S_4$     |      |      | s11  |      |        |
| $S_5$     | s12  |      |      |      |        |
| $S_6$     |      |      |      |      | accept |
| $S_{710}$ | r1   |      | r2   |      |        |
|           | r2   |      | r1   |      |        |
| $S_8$     |      |      |      |      | r3     |
| $S_9$     |      |      |      |      | r4     |
| $S_{11}$  |      |      |      |      | r5     |
| $S_{12}$  |      |      |      |      | r6     |

So this grammar is not LALR(1).