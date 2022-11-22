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

## 3. Regular description for $\mathtt{SWAP}(\\{ a^ib^jc^k \mid i,j,k\geq 0 \\})$

Give a regular description for the language of the words that can be obtained by swapping exactly two symbols on a word of the form $a^i b^j c^k$ for $i,j,k \ge 0$.

```c++
main
{
	a = "a"; b = "b"; c = "c";
  	l = (a | b | c);
  	
  	NOT_SWAP = a b c | a b | b c | a c | l | "";
  	PERMS = a* b a* b* a b* c* | a* b* c b* c* b c* | a* c a* b* c* a c* | a* b* c*; 
  	
  	output PERMS - NOT_SWAP; 
}
```

## 4. Regular description (with at most $500$ characters) for the finite language $\\{ xy \in \\{a,b,c,d\\}^* \mid |x|=|y| \wedge \forall s\in\\{a,b,c,d\\}: (|x|\_s\leq 1 \wedge |y|\_s\leq 1) \\}$

Give a regular description (using at most $500$ characters in the description) for the set of words over $\\{a,b,c,d\\}$ of the form $xy$, where $x$ and $y$ are words with the same length and without repetitions of symbols.

```c++
main
{
	a = "a"; b = "b"; c = "c"; d = "d";
  	w = (a|b|c|d);
  	e = w*;
  
  	k = e a e a e;
  	l = e b e b e;
  	m = e c e c e;
  	n = e d e d e;
  	
  	f = e - l - m - n - k;
	
  	s2 = w w; s3 = w w w; s4 = w w w w;
  
  	output "" | (w w) | (f & s2) (f & s2) | (f & s3) (f & s3) | (f & s4) (f & s4);
}
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
