# Pushdown Automaton
## _Basic format describing PDAs_

A PDA is defined by (i) its initial stack symbol, (ii) its initial state, (iii) its set of accepting
states, and (iv) its transition rules. Hence, in order to describe a PDA we write in the first
line the information corresponding to (i), (ii) and (iii), and in the successive lines we write
the transition rules. For instance, with a first line like:

```py
Z q0 q0 q3
```

we specify that (i) the initial contents of the stack is the symbol $Z$, that (ii) the initial state
of the automaton is $q0$, and (iii) that the accepting states are $q0$ and $q3$. After that line, we
need to specify each of the transitions rules. To this end, we may use two different syntaxes. I'm only going to describe the one we'll be using:

```py
q1 -> Za|ZA, Aa|AA -> q1
```

## _RACSO exercises on PDAs_

### Exercise 1: Deterministic uniquely-acceptinfg PDA for $\\{ a^n b^n \mid n\geq 0 \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the language over $\\{a,b\\}$ where the first half of each word only contains $a$'s and the second half only contains $b$'s.

```py
Z I I T
I -> Za | ZA -> A
A -> Aa | AA -> A
A -> Ab |    -> B
B -> Ab |    -> B
B -> Z  | Z  -> T
```

