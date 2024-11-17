# Exercises 1.1

## Problem 1

### Problem Description

Check the distributive laws for $\cup$ and $\cap$ and DeMorgan’s laws.

### Solution

| $A$  | $B$  | $C$  | $A\cap(B\cup C)$ | $(A\cap B)\cup(A\cap C)$ |
| ---- | ---- | ---- | ---------------- | ------------------------ |
| F    | F    | F    | F                | F                        |
| F    | F    | T    | F                | F                        |
| F    | T    | F    | F                | F                        |
| F    | T    | T    | F                | F                        |
| T    | F    | F    | F                | F                        |
| T    | F    | T    | T                | T                        |
| T    | T    | F    | T                | T                        |
| T    | T    | T    | T                | T                        |

| $A$  | $B$  | $C$  | $A\cup(B\cap C)$ | $(A\cup B)\cap(A\cup C)$ |
| ---- | ---- | ---- | ---------------- | ------------------------ |
| F    | F    | F    | F                | F                        |
| F    | F    | T    | F                | F                        |
| F    | T    | F    | F                | F                        |
| F    | T    | T    | T                | T                        |
| T    | F    | F    | T                | T                        |
| T    | F    | T    | T                | T                        |
| T    | T    | F    | T                | T                        |
| T    | T    | T    | T                | T                        |

| $A$  | $B$  | $\neg(A\cup B)$ | $\neg A\cap\neg B$ |
| ---- | ---- | --------------- | ------------------ |
| F    | F    | T               | T                  |
| F    | T    | F               | F                  |
| T    | F    | F               | F                  |
| T    | T    | F               | F                  |

| $A$  | $B$  | $\neg(A\cap B)$ | $\neg A\cup\neg B$ |
| ---- | ---- | --------------- | ------------------ |
| F    | F    | T               | T                  |
| F    | T    | T               | T                  |
| T    | F    | T               | T                  |
| T    | T    | F               | F                  |

## Problem 2

### Problem Description

Determine which of the following statements are true for all sets $A,B,C$, and $D$. If a double implication fails, determine whether one or the other of the possible implications holds. If an equality fails, determine whether the statement becomes true if the “equals” symbol is replaced by one or the other of the inclusion symbols $\subset$ or $\supset$.

(a) $A\subset B$ and $A\subset C$ $\Leftrightarrow$ $A\subset(B\cup C)$.

(b) $A\subset B$ or $A\subset C$ $\Leftrightarrow$ $A\subset(B\cup C)$.

(c) $A\subset B$ and $A\subset C$ $\Leftrightarrow$ $A\subset(B\cap C)$.

(d) $A\subset B$ or $A\subset C$ $\Leftrightarrow$ $A\subset(B\cap C)$.

(e) $A-(A-B)=B$.

(f) $A-(B-A)=A-B$.

(g) $A\cap(B-C)=(A\cap B)-(A\cap C)$.

(h) $A\cup(B-C)=(A\cup B)-(A\cup C)$.

(i) $(A\cap B)\cup(A-B)=A$.

(j) $A\subset C$ and $B\subset D$ $\Rightarrow$ $(A\times B)\subset(C\times D)$.

(k) The converse of (j).

(l) The converse of (j), assuming that $A$ and $B$ are nonempty.

(m) $(A\times B)\cup(C\times D)=(A\cup C)\times(B\cup D)$.

(n) $(A\times B)\cap(C\times D)=(A\cap C)\times(B\cap D)$.

(o) $A\times (B-C)=(A\times B)-(A\times C)$.

(p) $(A-B)\times(C-D)=(A\times C-B\times C)-A\times D$.

(q) $(A\times B)-(C\times D)=(A-C)\times(B-D)$.

### Solution

#### (a) and (c)



