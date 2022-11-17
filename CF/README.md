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
### Exercise 6: Context-free description for $\\{ a^ib^ja^kb^ra^sb^t \mid i+k+s=j+r+t \\}$

Give a context-free description for the set of words of the form $a^i b^j a^k b^r a^s b^t$ such that $i+k+s=j+r+t$.

```c++
main
{
	EQ_AMOUNT = "S -> SaSbS | SbSaS |";
	
  	ORDER = "
		a  b
	A1	A1 B1 +
	B1	A2 B1 +
	A2	A2 B2 +
	B2	A3 B2 +
	A3	A3 B3 +
	B3	M  B3 +
	M	M  M
	";
  
  	output EQ_AMOUNT & ORDER;
}
```

### Exercise 7: Context-free description for $\\{ a^ib^ja^kb^ra^sb^t \mid i+k+s=2(j+r+t) \\}$

Give a context-free description for the set of words of the form $a^i b^j a^k b^r a^s b^t$ such that $i+k+s=2(j+r+t)$.

```c++
main
{
	DOUBLE = "S -> SaSaSbS | SaSbSaS | SbSaSaS |";
	
  	ORDER = "
		a  b
	A1	A1 B1 +
	B1	A2 B1 +
	A2	A2 B2 +
	B2	A3 B2 +
	A3	A3 B3 +
	B3	M  B3 +
	M	M  M
	";
  
  	output DOUBLE & ORDER;
}
```

### Exercise 8: Context-free description for $\\{ a^ib^ja^kb^ra^sb^t \mid i+k+r+t=j+s \\}$

Give a context-free description for the set of words of the form $a^i b^j a^k b^r a^s b^t$ such that $i+k+r+t=j+s$

```c++
main
{
    ZFG = "S -> aCS | bCS | cQS | dQS |
    	   C -> aCC | bCC | c | d
	   Q -> a | b | cQQ | dQQ";
    
    // A C A B D B
    // Llavors A's + B's = C's + D's
    ORDER = "
		a  b  c d
	A1	A1 B1 C D +
	C	A2 B1 C D +
	A2	A2 B1 M D +
	B1	M  B1 M D +
	D	M  B2 M D +
	B2	M  B2 M M +
	M	M  M  M M
	";
  
    output substitution(ZFG & ORDER, "c"->"b", "d"->"a");

}
```

### Exercise 9: Context-free description for $\\{ w_1aw_2aw_3 \mid w_1,w_2,w_3\in\\{0,1\\}^*\ \wedge\ |w_1|=|w_2|_0+|w_3|_1\ \wedge\ |w_1w_2|_{111}\geq 1 \\}$


Give a context-free description for the set of words of the form $w_1aw_2aw_3$ such that $w1$, $w2$, $w3$ are constructed over the alphabet $\\{0,1\\}$, the size $w_1$​ coincides with the number of $0$'s of $w_2$ plus the number of $1$'s of $w_3$​, and $w_1w_2$​ has at least one occurrence of $111$.

```c++
main
{
	ZFG = "S -> Ta | XS1 | S0 
	       X -> 0 | 1
	       T -> XT0 | T1 | a";
  
  	TRIPLE_1 = "	
		0  1  a
	0	0  1  0A
	0A	0A 1A M
	1	0  2  1A
	1A	0A 2A M
	2	0  Y  2A
	2A	0A Y  M
	Y	Y  Y  Y +
	M	M  M  M
	";
    
  	output (ZFG & TRIPLE_1);
  
}
```

