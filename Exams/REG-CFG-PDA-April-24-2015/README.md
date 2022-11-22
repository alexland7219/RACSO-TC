# Exam on REGs, CFGs and PDAs, April 24th, 2015

## 1. Context-free description for $\\{ xcy \mid x,y\in \\{a,b\\}^* \wedge |x|=|y| \wedge |xcy|\_a\leq 5 \\}$

Give a context-free description for the set of words $w$ of the form $xcy$, for words $x$, $y$ over $\\{a,b\\}$ with identical length, and such that the total number of occurrences of $a$ in $w$ does not exceed $5$.

```c++
main
{
	ZFG = "S -> aSa | bSb | aSb | bSa | c";
  	
  	MOST_5_A = "
		a b c
	0	1 0 0 +
	1	2 1 1 +
	2	3 2 2 +
	3	4 3 3 +
	4	5 4 4 +
	5	M 5 5 +
	M	M M M
	";
  
  	output ZFG & MOST_5_A;
}
```

## 2. Deterministic uniquely-accepting PDA for well-parenthesized words over $\\{(,)\\}$ that terminate with $))$

Write a **deterministic uniquely-accepting** PDA recognizing the set of well-parenthesized words $w$ over $\\{(,)\\}$ and of the form $w=x))$ for some word $x$.

```ruby
Z 1 2
1 -> Z( | ZK, K( | KN, N( | NO, O( | OO -> 1
1 -> K) | -> 1
1 -> O) | -> 1
1 -> N) | T -> 1
1 -> T( | N -> 1
1 -> T) | -> 2
2 -> K( | K -> 1 
```

## 5. Deterministic uniquely-accepting PDA (with at most $2$ states) for well-parenthesized words over $\\{(,)\\}$ that terminate with $))$

Write a **deterministic uniquely-accepting** PDA with at most $2$ states recognizing the set of well-parenthesized words $w$ over $\\{(,)\\}$ and of the form $w=x))$ for some word $x$.

```ruby
Z 1 2
1 -> Z( | ZK, K( | KN, N( | NO, O( | OO -> 1
1 -> K) | -> 1
1 -> O) | -> 1
1 -> N) | T -> 1
1 -> T( | N -> 1
1 -> T) | -> 2
2 -> K( | K -> 1 
```
