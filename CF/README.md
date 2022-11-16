# Context-free Operations

## _Basic format for describing Context-free languages_

The format extends the previous one by adding the option to have context-free grammars as basic literals.

There are only two restrictions:

- $L & K$ is invalid when $L$ and $K$ are both context-free languages.
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