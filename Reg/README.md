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


### Exercise 4: Regular description for $\\{ w \in \\{a,b\\}^* \mid |w|\_\{aba\}=|w|\_\{bab\}=1 \\}$

Give a regular description for the set of words over $\\{a, b\\}$ such there is exactly one occurrence of $aba$ and of $bab$.

```c++
main
{

  	oneABA = "
			a   b 
		I	A   I
		A	A   AB
		AB	YA  I
		YA  YA  C +
		C	M   YB +
		YB  YA  YB +
		M	M   M
	";
  
    	oneBAB = substitution(oneABA, "a"->"b", "b"->"a");

  
	output oneABA & oneBAB ; 
}
```

_Note: I've given just one possible solution. There's many more as I've shown before_

### Exercise 5: Regular description for $\\{ w \in \\{a,b\\}^* \mid \exists w_1,w_2: (w=w_1aw_2\ \wedge\ |w_2|=5)\ \wedge\ |w|\_\{bbb\}&gt;0 \\}$

Give a regular description for the set of words over $\\{a, b\\}$ such that there is an $a$ at positions six from the end, and there is at least one occurrence of $bbb$.

```c++
main
{
    oneBBB = "
			a  b 
		I	I  A 
		A	I  AA
		AA	I  Y 
		Y   Y  Y +
	";

  	a = "a";
  	b = "b";
  	ab = a | b;
  
	output ab* a ab ab ab ab ab & oneBBB ; 
}
```

### Exercise 6: Regular description for $\\{ w \in \\{0,1\\}^* \mid \mathtt{value}_2(w)\in\dot{12}\\}$

Give a regular description for the set of words $w$ over $\\{0,1\\}$ such that the natural value obtained by interpreting $w$ as a binary number, that is $\mathtt{value}_2(w)$, is multiple of $12$ (in particular, the empty word represents $0$, which is multiple of $12$).

```c++
main
{
	mult3 = "
		0 1
	Z	Z U +
	U 	D Z 
	D 	U D
	";
  
  	mult4 = "
		0 1
	K	K N +
	N 	T N
	T	K N
	";
	  
	output mult3 & mult4;
}
```

_Note: Multiples of 12 are those multiples of 3 and 4 simultaneously_

### Exercise 7: Regular description for $\\{ w \in \\{0,1\\}^* \mid \mathtt{value}_2(w)\in\dot{20}\\}$

Give a regular description for the set of words $w$ over $\\{0,1\\}$ such that the natural value obtained by interpreting $w$ as a binary number, that is $\mathtt{value}_2(w)$, is multiple of $20$ (in particular, the empty word represents $0$, which is multiple of $20$).

```c++
main
{
    	mult4 = "
		0 1
	K	K N +
	N 	T N
	T	K N
	";
	
  	mult5 = "
		0 1
	Z	Z U +
	U	D T 
	D	Q Z
	T  	U D
	Q	T Q
	";
  
  	output mult4 & mult5;
}
```

_Note: Multiples of 20 are those multiples of 4 and 5 simultaneously_

### Exercise 8: Regular description for $\\{ w \in \\{0,1\\}^* \mid \mathtt{value}_2(w)\in\dot{60}\\}$

Give a regular description for the set of words $w$ over $\\{0,1\\}$ such that the natural value obtained by interpreting $w$ as a binary number, that is $\mathtt{value}_2(w)$, is multiple of $60$ (in particular, the empty word represents $0$, which is multiple of $60$).

```c++
main
{
  	mult4 = "
                0 1
        K       K N +
        N       T N
        T       K N
        ";

        mult5 = "
                0 1
        Z       Z U +
        U       D T
        D       Q Z
        T       U D
        Q       T Q
        ";
        mult3 = "
                0 1
        Z       Z U +
        U       D Z
        D       U D
        ";
  
  	    output mult3 & mult4 & mult5;
}
```

_Note: Multiples of 60 are those multiples of 4, 5 and 3 simultaneously_


### Exercise 9: Regular description for $\sigma(L)$ where $L=\\{ w \in \\{a,b\\}^* \mid \exists x,y: (w=xay\ \wedge\ |y|=2) \\}$ and $\sigma$ is the morphism defined by $\sigma(a)=aba$ and $\sigma(b)=bab$

Give a regular description for the image of the set of words over $\\{a, b\\}$, with an $a$ in the third position starting from the end, through the morphism $\sigma$ defined by $\sigma(a)=aba$ and $\sigma(b)=bab$.

```c++
main 
{
    a = "aba";
    b = "bab";
    ab = a | b;

    reg = ab* a ab ab;

    output reg;
}
```

_Note: By replacing the variables a and b we implicitly do a substitution_

### Exercise 10: Regular description for $\sigma(L)$ where $L=\\{ w \in \\{a,b,c\\}^* \mid \exists x,y: ((w=xay\ \vee\ w=xcy)\ \wedge\ |y|=1) \\}$ and $\sigma$ is the morphism defined by $\sigma(a)=aba$, $\sigma(b)=aa$ and $\sigma(c)=b$

Give a regular description for the image of the set of words over $\\{a, b, c\\}$, with either an $a$ or a $c$ in the second position starting from the end, through the morphism $\sigma$ defined by $\sigma(a)=aba$, $\sigma(b)=aa$ and $\sigma(c)=b$.

```c++
main
{
	a = "aba";
  	b = "aa";
  	c = "b";
  
  	abc = a | b | c;
  	ac  = a | c;
  
  	output abc* ac abc;
}
```

### Exercise 11: Regular description for $\sigma(L)$ where $L=\\{ w \in \\{a,b\\}^* \mid \exists x,y: (w=xay\ \wedge\ |y|=2) \\}$ and $\sigma$ is the substitution defined by $\sigma(a)=\\{aa\\}^*$ and $\sigma(b)=\\{a,aba,bab\\}$

Give a regular description for the image of the set of words over $\\{a, b\\}$, with an $a$ in the third position starting from the end, through the substitution $\sigma$ defined by $\sigma(a)=\\{aa\\}^*$ and $\sigma(b)=\\{a,aba,bab\\}$.

```c++
main
{
	a = "aa"*;
  	b = "a" | "aba" | "bab";
  
  	ab = a | b;
  
  	output ab* a ab ab;
}
```

### Exercise 12: Regular description for the language recognized by the NFA with set of states $\\{0,1,2,3,4,5\\}$, initial state $0$, accepting state $4$, and transitions $\delta(0,a)=\\{1,3\\}$, $\delta(0,b)=4$, $\delta(1,a)=4$, $\delta(1,b)=\\{2,3\\}$, $\delta(2,b)=5$, $\delta(3,a)=2$, $\delta(4,a) = \\{0,5\\}$, $\delta(4,b)=\\{0,2\\}$, $\delta(5,a)=4$

Give a regular description for the language recognized by the NFA represented here:

<p align="center">
<img src="https://i.imgur.com/SkKNhAJ.png" alt="NFA Exercise 12">
</p>
