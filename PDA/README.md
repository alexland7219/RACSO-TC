# Pushdown Automaton
## _Basic format describing PDAs_

A PDA is defined by (i) its initial stack symbol, (ii) its initial state, (iii) its set of accepting
states, and (iv) its transition rules. Hence, in order to describe a PDA we write in the first
line the information corresponding to (i), (ii) and (iii), and in the successive lines we write
the transition rules. For instance, with a first line like:

```ruby
Z q0 q0 q3
```

we specify that (i) the initial contents of the stack is the symbol $Z$, that (ii) the initial state
of the automaton is $q0$, and (iii) that the accepting states are $q0$ and $q3$. After that line, we
need to specify each of the transitions rules. To this end, we may use two different syntaxes. I'm only going to describe the one we'll be using:

```ruby
q1 -> Za|ZA, Aa|AA -> q1
```

## _RACSO exercises on PDAs_

### Exercise 1: Deterministic uniquely-accepting PDA for $\\{ a^n b^n \mid n\geq 0 \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the language over $\\{a,b\\}$ where the first half of each word only contains $a$'s and the second half only contains $b$'s.

```ruby
Z I I T
I -> Za | ZA -> A
A -> Aa | AA -> A
A -> Ab |    -> B
B -> Ab |    -> B
B -> Z  | Z  -> T
```

_Note: For every a we read, we push an **A** onto the stack_

### Exercise 2: Deterministic uniquely-accepting PDA for $\\{ a^\{2n\} b^n \mid n\geq 0 \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words of the form $a^{2n} b^n$, with $n \ge 0$.

```ruby
Z I I T
I -> Za | ZI -> A
A -> Pa | PI, Ia | IP -> A
A -> Pb | -> B
B -> I |, Pb | -> B
B -> Z | Z -> T
```

### Exercise 3: Deterministic uniquely-accepting PDA for $\\{ w \in \\{a,b\\}^* \mid |w|\_a=|w|\_b \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words over $\\{a,b\\}$ such that the number of occurrences of $a$ coincides with the number of occurrences of $b$.

```ruby
Z I I
I -> Za | ZA -> A
I -> Zb | ZB -> B
A -> Aa | AA, Ab | -> A
A -> Z | Z -> I
B -> Bb | BB, Ba | -> B
B -> Z | Z -> I
```

### Exercise 4: Deterministic uniquely-accepting PDA for $\\{ w \in \\{a,b\\}^* \mid |w|\_a\neq|w|\_b \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words over $\\{a,b\\}$ such that the number of occurrences of $a$ is different from the number of occurrences of $b$.


```ruby
Z I A B
I -> Za | ZX -> A
I -> Zb | ZX -> B
A -> Xa | XA, Aa | AA, Ab | -> A
B -> Xb | XB, Bb | BB, Ba | -> B
A -> Xb | -> I
B -> Xa | -> I
```

### Exercise 5: Deterministic uniquely-accepting PDA for $\\{ w \in \\{a,b\\}^* \mid |w|\_a\geq|w|\_b \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words over $\\{a,b\\}$ such that the number of occurrences of $a$ is greater than or equal to the number of occurrences of $b$.

```ruby
Z I I A
I -> Za | ZX -> A
I -> Zb | ZX -> B
A -> Xa | XA, Aa | AA, Ab | -> A
B -> Xb | XB, Bb | BB, Ba | -> B
A -> Xb | -> I
B -> Xa | -> I
```

### Exercise 6: Deterministic uniquely-accepting PDA for $\\{ w \in \\{a,b\\}^* \mid 2|w|\_a=|w|\_b \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words over $\\{a,b\\}$ such that the number of occurrences of $b$ is twice the number of occurrences of $a$.

```ruby
Z I I 
I -> Za | ZAA -> A
I -> Zb | ZB -> B
A -> Aa | AAA, Ab | -> A
A -> Z | Z -> I
B -> Bb | BB -> B
B -> Z | Z -> I
B -> Ba | -> R
R -> B | -> B
R -> Z | ZX -> M
M -> Z | Z -> I
M -> Xa | XXX, Xb | -> M
```

### Exercise 7: Deterministic uniquely-accepting PDA for $\\{ w \in \\{a,b\\}^* \mid 2|w|\_a\geq|w|\_b \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words over $\\{a,b\\}$ such that the number of occurrences of $b$ is at most twice the number of occurrencees of $a$.

```ruby
Z I I M A
I -> Za | ZAA -> A
I -> Zb | ZB -> B
A -> Aa | AAA, Ab |, Za | ZAA -> A
A -> Zb | ZB -> B
B -> Bb | BB -> B
B -> Z | Z -> I
B -> Ba | -> R
R -> B | -> B
R -> Z | ZX -> M
M -> Xa | XXX, Xb | -> M
M -> Za | ZAA -> A
M -> Zb | ZB -> B
```

### Exercise 8: Deterministic uniquely-accepting PDA for $\\{ w \in \\{a,b\\}^* \mid 2|w|\_a\leq|w|\_b \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words over $\\{a,b\\}$ such that the number of occurrences of $b$ is at least twice the number of occurrences of $a$.

```ruby
Z I I B 
I -> Za | ZAA -> A
I -> Zb | ZB -> B
A -> Aa | AAA, Ab | -> A
A -> Z | Z -> I
B -> Bb | BB, Zb | ZB -> B
B -> Za | ZAA -> A
B -> Ba | -> R
R -> B | -> B
R -> Z | ZX -> M
M -> Z | Z -> I
M -> Xa | XXX, Xb | -> M
```

### Exercise 9: Uniquely-accepting PDA for $\\{ a^i b^j \mid j\leq i\leq 2j \\}$

Write **uniquely-accepting** DFA (**which cannot be deterministic**) recognizing the words of the form $a^i b^j$ where the number of $a$'s is at least the number of $b$'s, but at most twice the number of $b$'s.

```ruby
Z I F
I -> Z | ZS -> P
P -> S | BSAA, T | BTA, S | T, T | -> P
P -> Aa |, Bb | -> P
P -> Z | -> F
```

### Exercise 10: Deterministic uniquely-accepting PDA for $\\{ w \in \\{a,b\\}^* \mid |w|\_{aa}=|w|\_b \\}$


Write a **deterministic uniquely-accepting** PDA recognizing the words over $\\{a,b\\}$ such that the number of occurrences of $aa$ coincides with the number of occurrences of $b$.

```ruby
Z 1 1 2
1 -> Za | Z -> 2
1 -> Zb | ZB -> 5
2 -> Zb | ZB -> 5 
2 -> Za | ZA -> 3
3 -> Aa | AA -> 3
3 -> Ab | -> 4
4 -> Aa | A -> 3
4 -> Ab | -> 4
4 -> Z | Z -> 1
5 -> Bb | BB -> 5
5 -> Ba | B -> 6
6 -> Ba | -> 6
6 -> Bb | BB -> 5
6 -> Z | Z -> 2
```

### Exercise 11: Deterministic uniquely-accepting PDA for $\\{ a^i b^j c^k \mid i=j+k \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words of the form $a^i b^j c^k$ such that the number of $a$'s coincides with the number of $b$'s plus the number of $c$'s.

```ruby
Z 1 1 F
1 -> Za | ZS -> 2
2 -> Sa | SS -> 2
2 -> Sb | -> 3
2 -> Sc | -> 4
3 -> Sb | -> 3
3 -> Sc | -> 4
3 -> Z | Z -> F
4 -> Sc | -> 4
4 -> Z | Z -> F
```

### Exercise 12: Deterministic uniquely-accepting PDA for $\\{ a^i b^j c^k \mid j=i+k \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words of the form $a^i b^j c^k$ such that the number of $b$'s coincides with the number of $a$'s plus the number of $c$'s.

```ruby
Z 1 1 I F
1 -> Za | ZY -> 2
1 -> Zb | ZN -> 4
2 -> Ya | YY -> 2
2 -> Yb | -> 3
3 -> Yb | -> 3
3 -> Z | Z -> I
I -> Zb | ZN -> 4
4 -> Nb | NN -> 4
4 -> Nc | -> 5
5 -> Nc | -> 5
5 -> Z | Z -> F
```

### Exercise 13: PDA for $\\{a^i b^j c^k \mid i=j \vee i=k \\}$

Write a PDA (**which will be non-deterministic and non-uniquely-accepting**) recognizing the words of the form $a^i b^j c^k$ with the same amount of $a$'s and $b$'s or the same amount of $a$'s and $c$'s.

```ruby
Z I F
I -> Z | ZS -> P
P -> S | KT, S | R -> P
P -> K | KC, K | -> P
P -> T | BTA, T | -> P
P -> R | CRA, R | V -> P
P -> V | VB, V | -> P
P -> Cc |, Bb |, Aa | -> P
P -> Z | Z -> F
```

### Exercise 14: PDA for $\\{a^i b^j c^k \mid i=j \vee j=k \\}$

Write a PDA (**which will be non-deterministic and non-uniquely-accepting**) recognizing the words of the form $a^i b^j c^k$ with the same amount of $a$'s and $b$'s or the same amount of $b$'s and $c$'s.

```ruby
Z I F
I -> Z | ZS -> P
P -> S | KM, S | NH -> P
P -> H | AH, H | -> P
P -> N | CNB, N | -> P
P -> K | CK, K | -> P
P -> M | BMA, M | -> P
P -> Aa |, Bb |, Cc | -> P
P -> Z | Z -> F
```

### Exercise 15: Uniquely-accepting PDA for $\\{ a^i b^j c^k d \mid i=j \\} \cup \\{a^i b^j c^k e\mid j=k \\}$

Write a **uniquely-accepting** PDA (**which cannot be deterministic**) recognizing the words of the form $a^i b^j c^k d$ with the same amount of $a$'s and $b$'s, and of the form $a^i b^j c^k e$ with the same amount of $b$'s and $c$'s.

```ruby
Z I F
I -> Z | ZS -> P
P -> S | DKJ, S | EHU -> P
P -> K | CK, K | -> P
P -> J | BJA, J | -> P
P -> H | CHB, H | -> P
P -> U | AU, U | -> P
P -> Aa |, Bb |, Cc |, Dd |, Ee | -> P
P -> Z | Z -> F
```

### Exercise 16: Uniquely-accepting PDA for $\\{ w \in \\{a,b\\}^* \mid w=w^R \\}$

Write a **uniquely-accepting** PDA (**which cannot be deterministic**) recognizing the palindromic words over $\\{a,b\\}$.

```ruby
Z I F
I -> Z | ZS -> P
P -> S | ASA, S | BSB, S | A, S | B, S | -> P
P -> Aa |, Bb | -> P
P -> Z | Z -> F
```

### Exercise 17: Deterministic uniquely-accepting PDA for the well-parenthesized words over $\\{ ( , ) \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the language of the well-paranthesized words over $\\{ ( , ) \\}$. For example, $()(())$ and $(((()())))$ are well-parenthesized words, whereas $)($ and $(()$ are not. One way to define more precisely this language is to describe it as the set of words that can be reduced to the empty word by successive applications of the rewrite rule $()\to\lambda$.

```ruby
Z 1 1
1 -> Z( | ZO -> 2
2 -> O( | OO -> 2
2 -> O) | -> 2
2 -> Z | Z -> 1
```

### Exercise 18: Deterministic uniquely-accepting PDA for the well-parenthesized words over $\\{ [ , ] , ( , ) \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the language of the well-paranthesized words over $\\{ [ , ] , ( , ) \\}$.

```ruby
Z 1 1
1 -> Z( | ZP, Z[ | ZB -> 2
2 -> P[ | PB, B( | BP, P) |, B] |, P( | PP, B[ | BB -> 2
2 -> Z | Z -> 1
```

### Exercise 19: Deterministic uniquely-accepting PDA for $\\{ xcy \mid x,y\in\\{a,b\\}^* \wedge |x|\_{a}=|y|\_{b} \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words of the form $xcy$, where $x$, $y$ are words over $\\{a,b\\}$ such that the number of occurrences of $a$ in $x$ is equal to the number of occurrences of $b$ in $y$.

```ruby
Z 1 F
1 -> Zb | Z, Za | ZA, Aa | AA, Ab | A -> 1
1 -> Zc | Z, Ac | A -> 2
2 -> Aa | A, Ab | -> 2
2 -> Z | Z -> F
F -> Za | Z -> F
```

### Exercise 20: Deterministic uniquely-accepting PDA for $\\{ xcy \mid x,y\in\\{a,b\\}^* \wedge |x|\_{ab}=|y|\_{ba} \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words of the form $xcy$, where $x$, $y$ are words over $\\{a,b\\}$ such that the number of occurrences of $ab$ in $x$ is equal to the number of occurrences of $ba$ in $y$.

```ruby
Z 1 F G 
1 -> Zb | Z, Ab | A -> 1
1 -> Za | Z, Aa | A -> 2
1 -> Zc | Z, Ac | A -> 3
2 -> Za | Z, Aa | A -> 2
2 -> Zb | ZA, Ab | AA -> 1
2 -> Zc | Z, Ac | A -> 3
3 -> Aa | A -> 3
3 -> Ab | A -> 4
3 -> Z | Z -> F
4 -> Ab | A -> 4
4 -> Aa | -> 3
F -> Za | Z -> F
F -> Zb | Z -> G
G -> Zb | Z -> G
```
### Exercise 21: Deterministic uniquely-accepting PDA for $\\{ xcy \mid x,y\in\\{a,b\\}^* \wedge |x|\_{aba}=|y|\_{bab} \\}$


Write a **deterministic uniquely-accepting** PDA recognizing the words of the form $xcy$, where $x$, $y$ are words over $\\{a,b\\}$ such that the number of occurrences of $aba$ in $x$ is equal to the number of occurrences of $bab$ in $y$.

```ruby
Z 1 7 8 9 Q
1 -> Zb | Z, Ab | A -> 1
1 -> Aa | A, Za | Z -> 2
2 -> Aa | A, Za | Z -> 2
2 -> Zb | Z, Ab | A -> 3
3 -> Zb | Z, Ab | A -> 1
3 -> Za | ZA, Aa | AA -> 2
1 -> Zc | Z, Ac | A -> 4
2 -> Zc | Z, Ac | A -> 4
3 -> Zc | Z, Ac | A -> 4
4 -> Aa | A -> 4
4 -> Z | Z -> 8
4 -> Ab | A -> 5
5 -> Ab | A -> 5
5 -> Aa | A -> 6
5 -> Z | Z -> 7
6 -> Ab | -> 5
6 -> Aa | A -> 4
7 -> Zb | Z -> 7
7 -> Za | Z -> 9
8 -> Za | Z -> 8
8 -> Zb | Z -> 7
9 -> Za | Z -> Q
Q -> Za | Z -> Q
Q -> Zb | Z -> 7
```