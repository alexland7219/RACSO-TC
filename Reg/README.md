# Regular Operations

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
