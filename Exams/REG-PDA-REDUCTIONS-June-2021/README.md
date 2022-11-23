# Exam on REGs, PDAs and Reductions, June 4th, 2021

## 1. Regular description for $\\{ w \in \\{a,b\\}^* \mid |w|\_{abba}=1\ \wedge\ (|w|\_{aaa}=0\ \vee\ |w|\_{bbb}\geq 2) \\}$

Give a regular description for the set of words over $\\{a,b\\}$ such there is exactly one occurrence of $abba$, and moreover there is no occurrence of $aaa$ or there are at least two occurrences of $bbb$.

```c++
main
{
	a = "a"; b = "b"; l = a | b;
  
	ONE_ABBA = "
		a b
	0	1 0 
	1	1 2
	2	1 3 
	3	5 0
	4	5 4 +
	5	5 6 +
	6	5 7 +
	7	M 4 +
	M	M M
	";
  
  	NO_AAA = l* - l* a a a l*;
  
  	MORE_THAN_ONE_BBB = l* b b b l* b b b l* | l* b b b b l*;
  
  	output ONE_ABBA & (NO_AAA | MORE_THAN_ONE_BBB);
}
```

## 2. Regular description for $\\{ w \in \\{0,1\\}^* \mid \mathtt{value}_2(w)\in\dot{12} \wedge \mathtt{value}_2(w^R)\in\dot{24}\\}$

Give a regular description for the set of words $w$ over $\\{0,1\\}$ such that the natural value obtained by interpreting $w$ as a binary number, that is $\mathtt{value}_2(w)$, is multiple of $12$, and the natural value obtained by interpreting the reverse of $w$ as a binary number is multiple of $24$. The empty word represents $0$.

```c++
main
{
	MULT_3 = "
		0 1
	0	0 1 +
	1	2 0
	2	1 2 
	";
  
  	MULT_4 = "" | "0" | ("0"|"1")* "0" "0";
  
  	MULT_8 = "" | "0" | "00" | ("0"|"1")* "0" "0" "0";
  
  	MULT_24_REV = reverse(MULT_3 & MULT_8);
  
  	output MULT_3 & MULT_4 & MULT_24_REV;
}
```

## 3. Uniquely-accepting PDA for $\\{w w^R \in \\{a, b\\} \mid | w w^R |_{aa} = 0\\}$

Write a **uniquely-accepting** PDA (**which cannot be deterministic**) recognizing the set of palindromic words over $\\{a,b\\}$ with even length and with no occurrence of $aa$.

```ruby
// CFG
// S -> bSb | aTa | 
// T -> bSb

Z I F
I -> Z | ZS -> P
P -> S | BSB, S | ATA, S | -> P
P -> T | BSB -> P
P -> Bb |, Aa | -> P
P -> Z | Z -> F
```

## 4. Reduction $\neg K \leq \\{p \mid | \mathtt{Dom}(\varphi_p) | = \infty \wedge \overline{| \mathtt{Dom}(\varphi_p) |} = \infty\\}$

Reduce $\neg K$ to the set of natural numbers codifying programs such that the domain and the complement of the domain of the function computed by the program have infinite cardinal (roughly, the set of programs implementing functions whose domain and complement of domain are infinite), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
	if (not mxxstopsininputsteps)
		if (y % 2 == 0) accept;
  		else reject;
  	else accept;
}
```

