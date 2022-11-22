# Exam on REGs, CFGs and PDAs, April 25th, 2016

## 1. Context-free description for $\\{ xcy \mid x,y\in \\{a,b\\}^*\ \wedge\ |x|=|y|\ \wedge \(|x|\_{aa}&gt;0\ \vee\ |y|\_{bb}&gt;0) \\}$

Give a context-free description for the set of words $w$ of the form $xcy$, for words $x$, $y$ over $\\{a,b\\}$ with identical length, and such that either there is at least one occurrence of $aa$ in $x$, or there is at least one occurrence of $bb$ in $y$.

```c++
main
{
	ZFG = "S -> aSb | bSa | aSa | bSb | c";
  	
  	a = "a"; b = "b"; c = "c";
  	
  	OOT = (a|b)* a a (a|b)* c (a|b)* | (a|b)* c (a|b)* b b (a|b)*;
  	
  	output ZFG & OOT;
}
```

## 2. Regular description for $\\{ w \in \\{0,1\\}^* \mid (|w|-2\in\dot{4})\ \vee\ (\mathtt{value}_2(w)\in\dot{5})\\}$

Give a regular description for the set of words $w$ over $\\{0,1\\}$ such that the length of $w$ is a multiple of $4$ plus $2$, or the natural value obtained by interpreting $w$ as a binary number, that is $\mathtt{value}_2(x)$, is multiple of $5$.

```c++
main
{
	MULT5 = "
		0  1
	M0	M0 M1 +
	M1	M2 M3
	M2	M4 M0
	M3	M1 M2
	M4	M3 M4
	";
  
  	LENGTH_MOD2 = "
		0  1
	M2	M3 M3
	M3	M0 M0
	M0	M1 M1 +
	M1	M2 M2
	";
  
  	output MULT5 | LENGTH_MOD2;
}
```

## 3. Determinisitic uniquely-accepting PDA for $\\{ w \in \\{a,b\\}^* \mid 2|w|\_a=3|w|\_b \\}$

Write a **deterministic uniquely-accepting** PDA recognizing the words over $\\{a,b\\}$ such that three times the number of occurrences of $b$ is twice the number of occurrences of $a$.

```ruby
// We let
// C = A²
// D = AB
// E = A²B

Z I I
I -> Za | Z -> A
I -> Zb | Z -> B
A -> Za | Z, Aa | A, Ba | B -> C
A -> Zb | Z, Ab | A, Bb | B -> D
C -> Aa | AA, Ba |, Za | ZA -> S
C -> Ab | A, Bb | B, Zb | Z -> E
B -> Zb | ZB, Bb | BB, Ab | -> S
B -> Za | Z, Ba | B, Aa | A ->  D
D -> Za | Z, Aa | A, Ba | B -> E
D -> Zb | ZB, Ab |, Bb | BB -> A
E -> Za | ZA, Aa | AA, Ba | -> B
E -> Zb | ZB, Ab | , Bb | BB -> C
S -> Aa | A, Ba | B -> A
S -> Ab | A, Bb | B -> B
S -> Z | Z -> I
```