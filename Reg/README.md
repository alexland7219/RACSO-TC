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

Give a regular description for the language recognized by the NFA represented [here](https://racso.lsi.upc.edu/juezwsgi/pics/exercise-nfa1.png).

```c++
main
{
 	DFA = " 	a	b
            1	24	5
            0	0	0
            3	0	6
            13	24	56
            24	35	34
            34	3	6
            134	234	56
            234	35	346
            5	16	13 +
            35	16	136 +
            135	1246	1356 +
            245	1356	134 +
            345	136	136 +
            1345	12346	1356 +
            2345	1356	1346 +
            6	5	0
            16	245	5
            136	245	56
            1246	2345	345
            346	35	6
            1346	2345	56
            12346	2345	3456
            56	156	13 +
            156	12456	135 +
            1356	12456	1356 +
            12456	123456	1345 +
            3456	1356	136 +
            13456	123456	1356 +
            123456	123456	13456 +
        ";
  
    output DFA;
}
```

_Note: This is the solution (yes really) if we were to convert the NFA to a DFA. A better solution of course would be to just make up new symbols for repeated transitions:_

```c++
main 
{
    DFA = "
            a c b d
        0   1 3 4 4
        1   4 4 2 3
        2   X X 5 5
        3   2 2 X X
        4   0 5 2 0 +
        5   4 4 X X
        X   X X X X
    ";

    output substitution(DFA, "c"->"a", "d"->"b");
}
```

### Exercise 13: Regular description for the language recognized by the NFA with set of states $\\{0,1,2,3,4,5\\}$, initial states $\\{2,5\\}$, accepting state $4$, and transitions $\delta(0,a)=\\{1,3\\}$, $\delta(0,b)=4$, $\delta(1,a)=4$, $\delta(1,b)=\\{2,3\\}$, $\delta(2,b)=5$, $\delta(3,a)=2$, $\delta(4,a) = \\{0,5\\}$, $\delta(4,b)=\\{0,2\\}$, $\delta(5,a)=4$

Give a regular description for the language recognized by the NFA represented [here](https://racso.lsi.upc.edu/juezwsgi/pics/exercise-nfa2.png).

```c++
main
{
	DFA1 = 
	  "
	  	a x b y 
	2	M M 5 5
	0	1 3 4 4
	1	4 4 2 3
	3	2 2 M M 
	4	0 5 2 0 +
	5	4 4 M M 
	M 	M M M M
	  ";
  
  	DFA2 = 
	  "
	  	a x b y 
	5	4 4 M M
	2	M M 5 5
	0	1 3 4 4
	1	4 4 2 3
	3	2 2 M M 
	4	0 5 2 0 +
	M 	M M M M
	  ";

  	langONE = substitution(DFA1, "x"->"a", "y"->"b");
  	langTWO = substitution(DFA2, "x"->"a", "y"->"b");
  
  	output langONE | langTWO;
}
```

_Note: One DFA for each possible initial state_

### Exercise 14: Regular description for $\\{a^n\mid n\in D\\}$, where $D$ is the set of distances of paths (with allowed repetition of nodes in the path) from node $0$ to node $4$ in the digraph with edges labelled with lengths whose set of nodes is $\\{0,1,2,3,4\\}$ and whose set of edges is $\\{0\xrightarrow{4}1,\ 1\xrightarrow{4}2,\ 1\xrightarrow{6}3,\ 2\xrightarrow{4}0,\ 2\xrightarrow{2}4,\ 3\xrightarrow{2}0,\ 4\xrightarrow{4}3\\}$

Give a regular description for $\\{a^n\mid n\in D\\}$, where $D$ is the set of distances of paths (with allowed repetition of nodes in the path) from node $0$ to node $4$ in the digraph with edges labelled with lengths that is represented [here](https://racso.lsi.upc.edu/juezwsgi/pics/exercise-len1.png).

```c++
main
{
	DFA = "
		a b c
	0	M 1 M
	1	M 2 3
	2	4 0 M
	3	0 M M
	4	M 3 M +
	M	M M M
	";
  
  	output substitution(DFA, "a" -> "aa", "b" -> "aaaa", "c" -> "aaaaaa");
}
```

_Note: Turn every lenght to a different symbol, then perform a substitution_

### Exercise 15: Regular description for $\\{a^n\mid n\in D\\}$, where $D$ is the set of distances of paths (with allowed repetition of nodes in the path) from node $0$ to node $5$ in the digraph with edges labelled with lengths whose set of nodes is $\\{0\xrightarrow{7}1,\ 0\xrightarrow{4}2,\  1\xrightarrow{7}1,\ 1\xrightarrow{9}3,\ 2\xrightarrow{4}4,\ 2\xrightarrow{3}5,\ 3\xrightarrow{4}0,\ 4\xrightarrow{5}2,\ 4\xrightarrow{3}3,\ 5\xrightarrow{9}4\\}$

Give a regular description for $\\{a^n\mid n\in D\\}$, where $D$ is the set of distances of paths (with allowed repetition of nodes in the path) from node $0$ to node $5$ in the digraph with edges labelled with lengths that is represented [here](https://racso.lsi.upc.edu/juezwsgi/pics/exercise-len2.png).


```c++
main
{
	DFA = "
		3 4 5 7 9
	0	M 2 M 1 M
	1	M M M 1 3
	2	5 4 M M M 
	3	M 0 M M M
	4	3 M 2 M M
	5	M M M M 4 +
	M 	M M M M M
	";
  
  	output substitution(DFA, "3" -> "aaa", "4" -> "aaaa", "5" -> "aaaaa", "7" -> "aaaaaaa", "9" -> "aaaaaaaaa");
}
```

### Exercise 16: Regular description for $\sigma(L)$ where $L=\\{ w \in \\{a,b\\}^* \mid |w|\_a\in\dot{2} \\}$ and $\sigma$ is the transducer with states $\\{0,1,2\\}$, initial state $0$, and transitions $0\xrightarrow{a\ |\ aba}1,\ 0\xrightarrow{b\ |\ bb}2,\ 1\xrightarrow{a\ |\ b}2,\ 1\xrightarrow{b\ |\ a}0,\ 2\xrightarrow{a\ |\ a}1,\ 2\xrightarrow{b\ |\ bbba}0$

Give a regular description for the image of the language $L=\\{ w \in \\{a,b\\}^* \mid |w|\_a\in\dot{2} \\}$ through the transducer represented [here](https://racso.lsi.upc.edu/juezwsgi/pics/exercise-transducer1.png). 

```c++
main
{
	DFA = "
		a  b  c  d  e  f
	P0	I1 P2 X  X  X  X +
	I0	P1 I2 X  X  X  X
	P1	X  X  I2 P0 X  X +
	I1	X  X  P2 I0 X  X
	P2	X  X  X  X  I1 P0 +
	I2	X  X  X  X  P1 I0
	X	X  X  X  X  X  X
	";
  
  	output substitution(DFA, "a" -> "aba", "b" -> "bb", "c" -> "b", "d" -> "a", "e" -> "a", "f" -> "bbba");
}
```

_Note: First build the DFA for L, then take into account the state of the transducer and new symbols for the translation_

### Exercise 17: Regular description for $\sigma(L)$ where $L=\\{ xay \in \\{a,b\\}^* \mid |y|=1 \\}$ and $\sigma$ is the transducer with states $\\{0,1\\}$, initial state $0$, and transitions $0\xrightarrow{a\ |\ aba}0,\ 0\xrightarrow{b\ |\ b}1,\ 1\xrightarrow{a\ |\ b}0,\ 1\xrightarrow{b\ |1\ aa}1$

Give a regular description for the image of the language $L=\\{ xay \in \\{a,b\\}^* \mid |y|=1 \\}$ through the transducer represented [here](https://racso.lsi.upc.edu/juezwsgi/pics/exercise-transducer2.png).

```c++
main
{
	DFA = "
		a  b  c  d
	A0	B0 A1 X  X
	A1	X  X  B0 A1
	B0	C0 D1 X  X
	B1	X  X  C0 D1
	C0	C0 D1 X  X  +
	C1	X  X  C0 D1 +
	D0	B0 A1 X  X  +
	D1	X  X  B0 A1 +
	X	X  X  X  X
	";
  
  	output substitution(DFA, "a" -> "aba", "c" -> "b", "d" -> "aa");
  
}
```

### Exercise 18: Regular description for $\\{ \mathtt{intercal}(w_1,w_2) \mid w_1,w_2\in\\{0,1\\}^*\ \wedge\ |w_1|=|w_2|\ \wedge\ \mathtt{value}_2(w_1)&gt;\mathtt{value}_2(w_2) \\}$, where $\mathtt{intercal}(a_1w_1,\ldots,a_nw_n)=a_1\ldots a_n\mathtt{intercal}(w_1,\ldots,w_n)$ and $\mathtt{intercal}(\lambda,\ldots,\lambda)=\lambda$

Give a regular description for the set of words obtained by intercaling two words $w_1$, $w_2$ over $\\{0,1\\}$ with the same length and such that the natural number obtained by interpreting $w_1$ as a binary number, that is $\mathtt{value}_2(w_1)$, is bigger than $\mathtt{value}_2(w_2)$.

```c++
main
{
	DFA = "
		0 1
	I	A B
	A	I M
	B	Y I
	Y	W W +
	W	Y Y
	M	M M
	";
  
 	output DFA;
}
```

_Notice: When intercaling two words, we read one symbol of the first one, then one of the other one, succcessively. We can easily build a DFA for this one_

### Exercise 19: Regular description for $\\{ \mathtt{intercal}(w_1,w_2) \mid w_1,w_2\in\\{0,1\\}^*\ \wedge\ |w_1|=|w_2|\ \wedge\ \mathtt{value}_2(w_1)&lt;\mathtt{value}_2(w_2) \\}$

Give a regular description for the set of words obtained by intercaling two words $w_1$, $w_2$ over $\\{0,1\\}$ with the same length and such that the natural number obtained by interpreting $w_1$ as a binary number, that is $\mathtt{value}_2(w_1)$, is smaller than $\mathtt{value}_2(w_2)$.

```c++
main
{
	DFA = "
		0 1
	I	A B
	A	I Y
	B	M I
	Y	W W +
	W	Y Y
	M	M M
	";
  
 	output DFA;
}
```

### Exercise 20: Regular description for $\\{ \mathtt{intercal}(w_1,w_2,w_3) \mid w_1,w_2,w_3\in\\{0,1\\}^*\ \wedge\ |w_1|=|w_2|=|w_3|\ \wedge\ \mathtt{value}_2(w_1)&gt;\mathtt{value}_2(w_2)&gt;\mathtt{value}_2(w_3) \\}$

Give a regular description for the set of words obtained by intercaling three words $w_1$, $w_2$, $w_3$ over $\\{0,1\\}$ with the same length and such that the natural number obtained by interpreting $w_1$ as a binary number, that is $\mathtt{value}_2(w_1)$, is bigger than $\mathtt{value}_2(w_2)$, that in addition is bigger than $\mathtt{value}_2(w_3)$.

```c++
main
{
	DFA = "
		a b c d e f g h
	A	A M M M B M C A
	B	B M Y B B M Y B 
	C	C C M M Y Y C C
	M	M M M M M M M M
	Y 	Y Y Y Y Y Y Y Y +
	";
  
  	output substitution(DFA, "a"->"000", "b"->"001", "c"->"010",
			    	 "d"->"011", "e"->"100", "f"->"101",
			    	 "g"->"110", "h"->"111");
  
}
```

_Note: Build a DFA by reading three symbols at a time_

### Exercise 21: Regular description for $\\{ \mathtt{intercal}(w_1,w_2,w_3) \mid w_1,w_2,w_3\in\\{0,1\\}^*\ \wedge\ |w_1|=|w_2|=|w_3|\ \wedge\ \mathtt{value}_2(w_1)&gt;\mathtt{value}_2(w_2)&lt;\mathtt{value}_2(w_3) \\}$

Give a regular description for the set of words obtained by intercaling three words $w_1$, $w_2$, $w_3$ over $\\{0,1\\}$ with the same length and such that the natural number obtained by interpreting $w_1$ as a binary number, that is $\mathtt{value}_2(w_1)$, is bigger than $\mathtt{value}_2(w_2)$, that in addition is smaller than $\mathtt{value}_2(w_3)$.


```c++
main
{
	DFA = "
		a b c d e f g h
	A	A B M M C Y M A
	B	B B M M Y Y B B  
	C	C Y M C C Y M C
	M	M M M M M M M M
	Y 	Y Y Y Y Y Y Y Y +
	";
  
  	output substitution(DFA, "a"->"000", "b"->"001", "c"->"010",
			    	 "d"->"011", "e"->"100", "f"->"101",
			    	 "g"->"110", "h"->"111");
  
}
```
### Exercise 22: Regular description for $\\{ \mathtt{intercal}(w_1,w_3) \mid \exists w_2: (w_1,w_2,w_3\in\\{0,1\\}^*\ \wedge\ |w_1|=|w_2|=|w_3|\ \wedge\ \mathtt{value}_2(w_1)&gt;\mathtt{value}_2(w_2)&gt;\mathtt{value}_2(w_3)) \\}$

Give a regular description for the set of words obtained by intercaling two words $w_1$, $w_3$ for which there exists another word $w_2$ such that all three $w_1$, $w_2$, $w_3$ satisfy that are words over $\\{0,1\\}$ with the same length and such that the natural number obtained by interpreting $w_1$ as a binary number, that is $\mathtt{value}_2(w_1)$, is bigger than $\mathtt{value}_2(w_2)$, that in addition is bigger than $\mathtt{value}_2(w_3)$.


```c++
main
{
	DFA = "
		a b c d e f g h
	A	A M M M B M C A
	B	B M Y B B M Y B 
	C	C C M M Y Y C C
	M	M M M M M M M M
	Y 	Y Y Y Y Y Y Y Y +
	";
  
  	output substitution(DFA, "a"->"00", "b"->"01", "c"->"00",
			    	 "d"->"01", "e"->"10", "f"->"11",
			    	 "g"->"10", "h"->"11");
  
}
```

_Note: It is very easy if we have solved Exercise 20 already_

### Exercise 23: Regular description for $\\{ \mathtt{intercal}(w_1,w_2,w_3) \mid w_1,w_2,w_3\in\\{0,1\\}^*\ \wedge\ |w_1|=|w_2|=|w_3|\ \wedge\ \mathtt{value}_2(w_1)+\mathtt{value}_2(w_2)=\mathtt{value}_2(w_3) \\}$

Give a regular description for the set of words obtained by intercaling three words $w_1$, $w_2$, $w_3$ over $\\{0,1\\}$ with the same length and such that the sum of the natural values obtained from $w_1$, $w_2$ by interpreting them as binary numbers, that is $\mathtt{value}_2(w_1)+\mathtt{value}_2(w_2)$, coincides with $\mathtt{value}_2(w_3)$.

```c++
main
{
	SUM = "
		a b c d e f g h
	N	N M M N M N C M +
	C	M N C M C M M C
	M	M M M M M M M M 
	";
  
  	REV = reverse(SUM);
  
  	output substitution(REV, "a"->"000", "b"->"001", "c"->"010",
			    	 "d"->"011", "e"->"100", "f"->"101",
			    	 "g"->"110", "h"->"111");
}
```

_Note: It is easier to add binary numbers from the end to the beginning of the word. Also **N** for no-carry and **C** for carry_