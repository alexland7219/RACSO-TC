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
_Note: Notice how the symbol **T** is a symbol that will generate zero or more b's forever_

### Exercise 5: Non-ambiguous CFG for $\\{ a^i b^j \mid 2i\leq j \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j$ where the number of $b$'s is at least twice the number of $a$'s.


```py
S -> aSbb | B
B -> Bb |
```

### Exercise 6: CFG for $\\{ a^i b^j \mid 2i\geq j \\}$

Write a CFG generating the words of the form $a^i b^j$ where the number of $b$'s is at most twice the number of $a$'s.

```py
S -> aSbb | aSb | aS |
```

_Note: In this case RACSO doesn't ask for non-ambiguity_

### Exercise 7: Non-ambiguous CFG for $\\{ a^i b^j \mid 2i\geq j \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j$ where the number of $b$'s is at most twice the number of $a$'s.

```py
S -> aSbb | aAb | A
A -> aA |
```

_Note: This is the previous exercise but without ambiguity._

### Exercise 8: Non-ambiguous CFG for $\\{ a^i b^j \mid j\leq i\leq 2j \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j$ where the number of $a$'s is at least the number of $b$'s, but at most twice the number of $b$'s.

```py
S -> aaSb | T
T -> aTb |
```

### Exercise 9: Non-ambiguous CFG for $\\{ a^i b^j \mid i\geq j \vee i\leq 2j \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j$ where the number of $a$'s is at least the number of $b$'s, or it is at most twice the number of $b$'s.

```py
S -> aSb | aA | Bb |
A -> aA |
B -> Bb |
```

_Note: Notice how_  $i \ge j \vee i \leq 2j$  _is always be true. Furthermore if the number of a's equals the number of b's and we need to generate the empty word from **S**, in order to avoid ambiguity with the empty word, we need **aA** instead of an **A** alone_

### Exercise 10: Non-ambiguous CFG for $\\{ a^i b^j c^k \mid i=j+k \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j c^k$ such that the number of $a$'s coincides with the number of $b$'s plus the number of $c$'s.

```py
S -> aSc | aKb |
K -> aKb |
```

_Note: We keep removing a's from the start and b's from the end until there are only a's and b's remaining, in which case we move to symbol **K**_

### Exercise 11: Non-ambiguous CFG for $\\{ a^i b^j c^k \mid j=i+k \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j c^k$ such that the number of $b$'s coincides with the number of $a$'s plus the number of $c$'s.

```py
S -> aTb | bQc | aTbbQc |
T -> aTb |
Q -> bQc |
```

_Note: Notice how symbols **T** and **Q** recognize_ $\\{a^x b^x\\}$ _and_ $\\{b^x c^x\\}$ _respectively_

### Exercise 12: CFG for $\\{ a^i b^j c^k \mid i=j \vee j=k \vee i=k \\}$

Write a CFG (**which will be ambiguous**) generating the words of the form $a^i b^j c^k$ where the number of $a$'s equals the number of $b$'s, or the number of $b$'s equals the number of $c$'s, or the number of $c$'s equals the number of $a$'s.

```py
S -> H | F | Z

H -> XC
F -> AY
Z -> aZc | B

A -> Aa |
B -> Bb |
C -> Cc |

X -> aXb |
Y -> bYc |
```

_Note: **H** will recognize those with_ $i = j$ _followed by a number of c's we don't care about. Same thing for case **F** recognizing the case_ $j=k$ _. Case **Z** is the last one, and we need to take care of the b's left inside the word._

### Exercise 13: CFG for $\\{ a^{n_0} b a^{n_1} b \ldots a^{n_{m-1}} b a^{n_m} \mid m\geq 1 \wedge \exists i\in\\{1,\ldots,m\\}: (n_0 = n_i) \\}$

Write a CFG (**which will be ambiguous**) generating the words of the form $a^\{n_0\}ba^\{n_1\}b\ldots a^\{n_\{m-1\}\} b a^\{n_m\}$ for which there exists an $i\in\\{1,\ldots,m\\}$ such that ${n_0}={n_i}$.

```py
S -> SbA | Y
Y -> aYa | bXb | b
X -> aX | bX | 
A -> Aa
```

_Note: From the beginning we can take two options. Either forget about the rightmost set of a's or take it and try to match every a from the beginning to every a from the end. We are introduced to a symbol that generates_ $\Sigma ^*$, **X**.

### Exercise 14: Non-ambiguous CFG for $\\{ a^\{n_0\} b a^\{n_1\} b \ldots a^\{n_\{m-1\}\} b a^\{n_m\} \mid m\geq 1 \wedge (n_0 = \sum_\{1\leq i\leq m\} n_i) \\}$

Write a **non-ambiguous** CFG generating the words of the form $a^\{n_0\}ba^\{n_1\}b\ldots a^\{n_\{m-1\}\} b a^\{n_m\}$, with $m \ge 1$, such that $n_0$ is equal to the sum $n_1 + n_2 + \ldots + n_m$.

```py
S -> aSa | Sb | b
```

### Exercise 15: CFG for $\\{ a^\{n_0\} b a^\{n_1\} b \ldots a^\{n_\{m-1\}\} b a^\{n_m\} \mid m\geq 1 \wedge \exists I\subseteq\\{1,\ldots,m\\}: (n_0 = \sum_\{i\in I\} n_i) \\}$

Write a CFG (**which will be ambiguous**) generating the words of the form $a^\{n_0\}ba^\{n_1\}b\ldots a^\{n_\{m-1\}\} b a^\{n_m\}$, with $m \ge 1$, for which $n_0$ is equal to the sum of a selection of naturals from $n_1, n_2, \ldots, n_m$, i.e., $n_0=\sum_\{i\in I\} n_i$ where $I\subseteq\\{1,\ldots,m\\}$. Note that, in particular, the selection might be empty, and therefore a word where $n_0$ is $0$ is necessarily correct.

```py
S -> K | SN | N
A -> aA | bA |
N -> bA
K -> aKa | Sb | b
```

### Exercise 16: Non-ambiguous CFG for $\\{ w \in \\{a,b\\}^* \mid w=w^R \\}$

Write a **non-ambiguous** CFG generating the palindromic words over $\\{a, b\\}$.

```py
S -> aSa | bSb | a | b |
```
### Exercise 17: Non-ambiguous CFG for $\\{ w \in \\{a,b\\}^* \mid w=w^R \wedge |w|_\{aba\}=0 \\}$

Write a **non-ambiguous** CFG generating the palindromic words over $\\{a, b\\}$ with no occurrence of $aba$.

```py
S -> aKa | bSb | a | b |
K -> bNb | aKa | a |
N -> bSb | b |
```
### Exercise 18: Non-ambiguous CFG for $\\{ w \in \\{a,b\\}^* \mid w=w^R \wedge |w|_a&gt;0 \wedge |w|_b&gt;0 \\}$

Write a **non-ambiguous** CFG generating the palindromic words over $\\{a, b\\}$ with some occurrence of $a$ and some occurrence of $b$.

```py
S -> aAa | bBb
A -> aAa | bPb | b
B -> bBb | aPa | a
P -> aPa | bPb | a | b |
```

_Note: Notice how **P** generates all palindromic words. We reach **P** once we've read at least one a and at least one b_

### Exercise 19: Non-ambiguous CFG for $\\{ w \in \\{a,b\\}^* \mid w=w^R \wedge |w|_\{aba\}&gt;0 \\}$

Write a **non-ambiguous** CFG generating the palindromic words over $\\{a, b\\}$ with some occurrence of $aba$.

```py
S -> aAa | bSb
A -> b | bBb | aAa
B -> a | bSb | aPa
P -> a | bPb | aPa | b |
```

### Exercise 20: CFG for the well-parenthesized words over $\\{ ( , ) \\}$

Write a CFG generating the language of the well-parenthesized words over $\\{ ( , ) \\}$. For example, $()(())$ and $(((()())))$ are well-parenthesized words, whereas $)($ and $(()$ are not. One way to define more precisely this language is to describe it as the set of words that can be reduced to the empty word by successive applications of the rewrite rule $()\to\lambda$.

```py
S -> S(S)S |
```

_Note: Notice how anything inside a parenthesis must be well-parenthesized, and same-level parenthesis can be concatenated._

### Exercise 21: CFG for the well-parenthesized words over $\\{ [ , ] , ( , ) \\}$

Write a CFG generating the language of the well-paranthesized words over $\\{ [ , ] , ( , ) \\}$. For example, $()[()]$ and $[[(()[])]]$ are well-paranthesized words, whereas $][$ and $(()$ are not. One way to define more precisely this language is to describe it as the set of words that can be reduced to the empty word by successive applications of the rewrite rules $()\to\lambda$ and $[]\to\lambda$.

```py
S -> S(S)S | S[S]S |
```

### Exercise 22: Non-ambiguous CFG for the well-parenthesized words over $\\{ ( , ) \\}$

Write a **non-ambiguous** CFG generating the language of the well-parenthesized words over $\\{ ( , ) \\}$. For example, $()(())$ and $(((()())))$ are well-parenthesized words, whereas $)($ and $(()$ are not. One way to define more precisely this language is to describe it as the set of words that can be reduced to the empty word by successive applications of the rewrite rule $()\to\lambda$.

```py
S -> (S)S |
```

### Exercise 23: Non-ambiguous CFG for the well-parenthesized words over $\\{ [ , ] , ( , ) \\}$

Write a **non-ambiguous** CFG generating the language of the well-paranthesized words over $\\{ [ , ] , ( , ) \\}$. For example, $()[()]$ and $[[(()[])]]$ are well-paranthesized words, whereas $][$ and $(()$ are not. One way to define more precisely this language is to describe it as the set of words that can be reduced to the empty word by successive applications of the rewrite rules $()\to\lambda$ and $[]\to\lambda$.

```py
S -> (S)S | [S]S |
```
