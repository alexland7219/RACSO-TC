# Context-Free Grammar
## _Basic format describing CFGs_

We describe this format by means of an example. Consider the following grammar:

```py
S -> aSb
S -> 
```
This grammar has a single non-terminal symbol S, two terminal symbols a and b, and two productions: the first one rewrites S into the word aSb, and the second one into the empty word. It is easy to see that the grammar generates the language $\\{a^n b^n \mid n \ge 0\\}$. Since both productions have the same left-hand side, they could be written in a single line like this:

```py
S -> aSb |
```

It is also possible to introduce more non-terminals, if this is considered necessary or convenient. For instance, the following grammar is equivalent to the previous example:
```py
S -> aXb |
X -> aSb |
```
We now give a more precise definition of the format. Grammars are described by a list of productions. A production starts with a non-terminal symbol, followed by ->, followed by the list of right-hand sides of such non-terminal separated by bars |. Each of the right-hand sides is a (possibly empty) list of symbols. A non-terminal symbol is an uppercase latin character, and a terminal symbol is any other character. We assume that the start symbol of the grammar is the first non-terminal to appear.

## _RACSO exercises on CFGs_

### Exercise 1: Non-ambiguous CFG for $\\{ a^n b^n \mid n\geq 0 \\}$

Write a **non-ambiguous** CFG generating the language over $\\{a, b\\}$ where the first half of each word only contains $a$'s and the second half only contains $b$'s.
```py
S -> aSb |
```

### Exercise 2: Non-ambiguous CFG for $\\{ a^n c b^n \mid n&gt;0 \\}$

Write a **non-ambiguous** CFG generating the words over $\\{a, b, c\\}$ such that there is an occurrence of $c$ exactly in the middle, to its left there are only $a$'s (and there is at least one $a$), and to its right there are only $b$'s (and there is at least one $b$). Note that, since the only occurrence of $c$ must be exactly in the middle, the number of $a$'s must be equal to the number of $b$'s.

```py
S -> aKb 
K -> aKb | c
```

### Exercise 3: Non-ambiguous CFG for $\\{ a^i b^j \mid i\geq j \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j$ where the number of $a$'s is at least the number of $b$'s.

```py
S -> aSb | T 
T -> aT |
```

_Note: We need two different symbols. Trying to merge everything into one would lead to ambiguity in the CFG_

### Exercise 4: Non-ambiguous CFG for $\\{ a^i b^j \mid i\leq j \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j$ where the number of $a$'s is at most the number of $b$'s.

```py
S -> aSb | T
T -> Tb |
```

### Exercise 5: Non-ambiguous CFG for $\\{ a^i b^j \mid 2i\leq j \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j$ where the number of $b$'s is at least twice the number of $a$'s.


```py
S -> aSbb | B
B -> Bb |
```

### Exercise 6: CFG for $\\{ a^i b^j \mid 2i\geq j \\}$