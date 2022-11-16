# Context-free Operations

## _Basic format for describing Context-free languages_

The format extends the previous one by adding the option to have context-free grammars as basic literals.

There are only two restrictions:

- $L\ \\&\ K$ is invalid when $L$ and $K$ are both context-free languages.
- $L - K$ is invalid when $K$ is a context-free language.

## _Exercises on Context-free Operations_

### Exercise 1: Context-free description for $\\{ w \in \\{a,b\\}^* \mid |w|_a=|w|\_b\ \wedge\ |w|\_{abba}&gt;0 \\}$

Give a context-free description for the set of words over $\\{a,b\\}$ with the same number of $a$'s as number of $b$'s, and with at least one occurrence of $abba$.

```c++
main
{
	ZFG = "S -> SaSbS | SbSaS |";
  
  	output ZFG & ("a"|"b")* "abba" ("a"|"b")*;
}
```

_Note: Build a CFG for the_ $|w|\_a=|w|\_b$ _part, then intersect it with a simple regular expression for the words containing_ $abba$.

### Exercise 2: Context-free description for $\\{ w \in \\{0,1\\}^* \mid w=w^R\ \wedge\ \mathtt{value}\_2(w)\in\dot{5} \\}$

Give a context-free description for the set of words over $\\{0,1\\}$ whose reverse are themselves and represent a multiple of $5$ as binary numbers.

```c++
main
{
	PAL = "S -> 0S0 | 1S1 | 0 | 1 |";
  	
  	MUL5 = "
		0  1
	M0	M0 M1 +
	M1	M2 M3
	M2	M4 M0
	M3	M1 M2
	M4	M3 M4
	";

  	output PAL & MUL5;
}
```

### Exercise 3: Context-free description for the well-paranthesized words over $\\{ ( , ) \\}$ with no occurrence of $((($.

Give a context-free description for the language of the well-parenthesized words over $\\{(,)\\}$ with no occurrence of $((($. For example, $()(())$ and $(((()())))$ are well-parenthesized words, whereas $)($ and $(()$ are not. Nevertheless, $(((()())))$ is not valid since it has occurrences of $((($. One way to define more precisely the language of well-parenthesized words over $\\{(,)\\}$ is to describe it as the set of words that can be reduced to the empty word by successive applications of the rewrite rule $()\to\lambda$.

```c++
main
{
	PAR = "S -> (S)S |";
  
  	NO_OC = "
		( )
	0	1 0 +
	1	2 0 +
	2	3 0 +
	3	3 3
	";
  
  	output PAR & NO_OC;
}
```

### Exercise 4: Context-free description for $\\{ \mathtt{intercal}(w_1,w_2) \mid w_1,w_2\in\\{a,b\\}^*\ \wedge\ |w_1|=|w_2|\ \wedge\ w_1=w_1^R\ \wedge\ |w_2|\_{aa}=0 \\}$

Give a context-free description for the set of words obtained by intercaling two words $w_1$, $w_2$ over $\\{a,b\\}$ with the same length, where $w_1$ is palindromic and with no occurrences of $aa$ in $w_2$.

```c++
main
{
	ZFG = "S -> aXSaX | bXSbX | aX | bX |
	       X -> a | b";
  
  	NO_AA = "
		a  b
	0A	0  0 +
	0	1A 0A
	1A	1  1 +
	1	2A 0A 
	2A	2A 2A 
	";
  
  	output ZFG & NO_AA;
}
```

### Exercise 5: Context-free description for $\\{ \mathtt{intercal}(w_1,w_2) \mid w_1,w_2\in\\{a,b\\}^*\ \wedge\ |w_1|=|w_2|\ \wedge\ |w_2|_{aa}=0\ \wedge\ \forall x_1,y_1,x_2,y_2:(w_1=x_1y_1\ \wedge\ w_2=x_2y_2\ \wedge\ |x_1|=|x_2|\ \Rightarrow\ |x_1|_a\geq|x_2|_a) \\}$

Give a context-free description for the set of words obtained by intercaling two words $w_1$, $w_2$ over $\\{a,b\\}$ with the same length and with no occurrences of $aa$ in $w_2$, and such that for each two prefixes $x_1$, $x_2$ of $w_1$, $w_2$, respectively, of the same length, it holds that $x_1$ has more or equal occurrences of $a$ than $x_2$.

```c++
main
{
  	NO_AA = "
		a  b
	0A	0  0 +
	0	1A 0A
	1A	1  1 +
	1	2A 0A 
	2A	2A 2A 
	";
  
  	EQ_PREF = "S -> aaS | bbS | abS | abSbaS |";
  
  	output NO_AA & EQ_PREF;
}
```
