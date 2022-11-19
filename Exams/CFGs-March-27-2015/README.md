# Exam on CFGs, March 27th, 2015

## 1. Non-ambiguous CFG for $\\{ w \in \\{a,b\\}^* \mid w=w^R \wedge |w|\_a\in\dot{2} \\}$

Write a **non-ambiguous** CFG generating the palindromic words where the number of occurrences of $a$ is even.

```py
S -> aSa | bSb | b |
```

## 2. Non-ambiguous CFG for $\\{ xcy \mid x,y\in\\{a,b\\}^* \wedge |x|=|y| \\wedge\ |x|\_a=2 \\}$

Write a **non-ambiguous** CFG generating the words of the form $xcy$, where $x$, $y$ are words over $\\{a,b\\}$ of the same length and such that the number of occurrences of $a$ in $x$ is $2$.

```py
S -> aXa | aXb | bSa | bSb
X -> bXb | bXa | aYb | aYa
Y -> c | bYb | bYa
```

## 3. Non-ambiguous CFG for $\\{a^i b^j c^k \mid 2j=i+k\\}$

Write a **non-ambiguous** CFG generating the words of the form $a^i b^j c^k$ such that twice the number of $b$'s coincides with the number of $a$'s plus the number of $c$'s.

```py
S -> aYbXc | YX
Y -> aaYb |
X -> bXcc |
```

## 4. CFG for $\\{ a^{n\_0} b a^{n\_1} b \ldots a^{n\_{m-1}} b a^{n\_m} \mid m\geq 1 \wedge \exists i:(1\leq i\leq m\ \wedge\ n\_0 = (\sum_{1\leq j\leq m} n\_j)-n\_i) \\}$

Write a CFG generating the words of the form $a^{n\_0}ba^{n\_1}b\ldots a^{n\_{m-1}} b a^{n\_m}$, with $m \ge 1$, such that $n_0$ is equal to the sum $n_1+n_2+\ldots+n_m$ minus a concrete $n_i$, for $1\leq i\leq m$.

