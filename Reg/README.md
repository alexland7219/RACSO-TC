# Regular Operations

## _Basic format for describing Regular languages_

The description is given in the <u>main</u> function. You can assign variables to languages, do operations such as the Union (|), Intersection (&), Kleene Star (*), and Concatenation (by leaving a space between languages).

One can define a language with Strings, or even DFA's following the format in Unit 1.

## _Exercises on Regular Operations_

### Exercise 1: Regular description for $\\{ w \in \\{a,b\\}^* \mid |w|\_{aaa}&gt;0\ \vee\ |w|\_{bbb}&gt;0\ \vee\ |w|\_{aba}&gt;0\ \vee\ |w|\_\{bab\}&gt;0 \\}$

Give a regular description for the set of words over $\\{a, b\\}$ such there is at least one occurrence of $aaa$ or $bbb$ or $aba$ or $bab$.

```c++
main
{
	a = "a";
  	b = "b";
  	ab = a | b;
  
  	L1 = ab* "aaa" ab*;
  	L2 = ab* "bbb" ab*;
  	L3 = ab* "aba" ab*;
  	L4 = ab* "bab" ab*;
	
  	output L1 | L2 | L3 | L4;
}
```

_Note: L1 is the language with aaa, L2 contains at least one bbb, L3 contains aba and L4 contains bab. The output is the union of all of these languages_

### Exercise 2: Regular description for $\\{ w \in \\{a,b\\}^* \mid |w|\_{aaa}&gt;0\ \wedge\ |w|\_{bbb}&gt;0\ \wedge\ |w|\_{aba}&gt;0\ \wedge\ |w|\_{bab}&gt;0 \\}$

Give a regular description for the set of words over $\\{a, b\\}$ such there is at least one occurrence of $aaa$ and of $bbb$ and of $aba$ and of $bab$.

```c++
main
{
	a = "a";
  	b = "b";
  	ab = a | b;
	
	L1 = ab* "aaa" ab*;
  	L2 = ab* "bbb" ab*;
  	L3 = ab* "aba" ab*;
  	L4 = ab* "bab" ab*;
  
  	output L1 & L2 & L3 & L4;
}
```

### Exercise 3: Regular description for $\\{ w \in \\{a,b\\}^* \mid |w|_\{aaa\}=|w|\_\{bbb\}=1 \\}$

Give a regular description for the set of words over $\\{a, b\\}$ such there is exactly one ocurrence of $aaa$ and of $bbb$.

```c++
main
{
    oneAAA = "
			a  b 
		I	A  I 
		A	AA I
		AA	Y  I 
		Y	M  N +
		M	M  M
		N	T  N +
		T	Y N +
	";
  
    	oneBBB = "
			a  b 
		I	I  A 
		A	I  AA
		AA	I  Y 
		Y	N  M +
		M	M  M
		N	N  T +
		T	N  Y +
	";
 
	output oneAAA & oneBBB ; 
}
```

_Note: This is the naive method. Intersection of two DFAs_


```c++
main
{
  	oneAAA = "
			a  b 
		I	A  I 
		A	AA I
		AA	Y  I 
		Y	M  N +
		M	M  M
		N	T  N +
		T	Y N +
	";
 
  	oneBBB = substitution(oneAAA, "a"->"b", "b"->"a");
  
	output oneAAA & oneBBB ; 
}
```

_Note: This is the second method (and the easiest). Substitute a's for b's and just create one DFA._


```c++
main
{
	a = "a";
  	b = "b";
  	L = "";
  
  	Y = ( b | a b | a a b )* a a a ( b ( b | a b ) * a a ) *;
  
  	reg1 = Y ( L | b ( b | a b ) * ( L | a ) );
  	reg2 = substitution(reg1, "a"->"b", "b"->"a");
  
  	output reg1 & reg2;
}
```

_Note: This is without DFAs after converting oneAAA to a Regular expression by hand_


### Exercise 4: Regular description for 