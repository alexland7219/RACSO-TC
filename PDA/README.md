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