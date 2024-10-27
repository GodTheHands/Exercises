# Exercises 4.5

## Problem 1

### Problem Description

For the grammar $S\rightarrow 0S1\;|\;01$ of Exercise 4.2.2(a), indicate the handle in each of the following right-sentential forms:

a) 000111.

b) 00S11.

### Solution

#### a)

Because
$$
S\Rightarrow 0S1\Rightarrow 00S11\Rightarrow 000111
$$
Therefore the handle is 01.

#### b)

Because
$$
S\Rightarrow 0S1\Rightarrow 00S11
$$
Therefore the handle is 0S1.

## Problem 2

### Problem Description

Repeat Exercise 4.5.1 for the grammar $S\rightarrow SS+\;|\;SS*\;|\;a$ of Exercise 4.2.1 and the following right-sentential forms:

a) $SSS+a*+$.

b) $SS+a*a+$.

c) $aaa*a++$.

### Solution

#### a)

Because
$$
S\Rightarrow SS+\Rightarrow SSS*+\Rightarrow SSa*+\Rightarrow SSS+a*+
$$
Therefore the handle is $SS+$.

#### b)

Because
$$
S\Rightarrow SS+\Rightarrow Sa+\Rightarrow SS*a+\Rightarrow Sa*a+\Rightarrow SS+a*a+
$$
Therefore the handle is $SS+$.

#### c)

Because
$$
S\Rightarrow SS+\Rightarrow SSS++\Rightarrow SSa++\Rightarrow SSS*a++\\
\Rightarrow SSa*a++\Rightarrow Saa*a++\Rightarrow aaa*a++
$$
Therefore the handle is $a$.

## Problem 3

### Problem Description

Give bottom-up parses for the following input strings and grammars:

a) The input 000111 according to the grammar of Exercise 4.5.1.

b) The input $aaa*a++$ according to the grammar of Exercise 4.5.2.

### Solution

#### a)

| Stack    | Input    | Action                       |
| -------- | -------- | ---------------------------- |
| \$       | 000111\$ | shift                        |
| \$0      | 00111\$  | shift                        |
| \$00     | 0111\$   | shift                        |
| \$000    | 111\$    | shift                        |
| \$0001   | 11\$     | reduce by $S\rightarrow 01$  |
| \$00$S$  | 11\$     | shift                        |
| \$00$S$1 | 1\$      | reduce by $S\rightarrow 0S1$ |
| \$0$S$   | 1\$      | shift                        |
| \$0$S$1  | \$       | reduce by $S\rightarrow 0S1$ |
| \$S      | \$       | accept                       |

#### b)

| Stack    | Input       | Action                        |
| -------- | ----------- | ----------------------------- |
| \$       | $aaa*a++\$$ | shift                         |
| $\$a$    | $aa*a++\$$  | replace by $S\rightarrow a$   |
| $\$S$    | $aa*a++\$$  | shift                         |
| $\$Sa$   | $a*a++\$$   | replace by $S\rightarrow a$   |
| $\$SS$   | $a*a++\$$   | shift                         |
| $\$SSa$  | $*a++\$$    | replace by $S\rightarrow a$   |
| $\$SSS$  | $*a++\$$    | shift                         |
| $\$SSS*$ | $a++\$$     | replace by $S\rightarrow SS*$ |
| $\$SS$   | $a++\$$     | shift                         |
| $\$SSa$  | $++\$$      | replace by $S\rightarrow a$   |
| $\$SSS$  | $++\$$      | shift                         |
| $\$SSS+$ | $+\$$       | replace by $S\rightarrow SS+$ |
| $\$SS$   | $+\$$       | shift                         |
| $\$SS+$  | $\$$        | replace by $S\rightarrow SS+$ |
| $\$S$$   | $\$$        | accept                        |