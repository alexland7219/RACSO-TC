# Exercises on reductions of programs

## _RACSO exercises on K-Reductions_

### Exercise 1: $K\ \leq\ \\{ p \mid \exists y:\ M_p(y){\downarrow} \\}$

Reduce $K$ to the set of natural numbers codifying programs such that the program halts with some input (roughly, the set of programs that halt with some input), in order to prove that such set is undecidable (not recursive).

```c
input y
{
    runmxx;
    accept;
}
```

### Exercise 2: $\neg K \leq\ \\{ p \mid \forall y:\ M\_p(y){\downarrow} \\}$

Reduce $\overline(K)$ to the set of natural numbers such that the program codified by them halts with any input (roughly, the set of programs that halt with any input), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
    if (mxxstopsininputsteps)
        infiniteloopp;
    
    accept;
}
```

### Exercise 3: $\neg K \leq\ \\{ p \mid \exists y:\ M\_p(y){\uparrow} \\}$

Reduce $\overline(K)$ to the set of natural numbers such that the program codified by them does not halt with some input (roughly, the set of programs non-halting with some input), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
    runmxx;
    accept;
}
```

### Exercise 4: $\neg K \leq\ \\{ p \mid \forall y:\ M\_p(y){\uparrow} \\}$

Reduce $\overline(K)$ to the set of natural numbers such that the program codified by them does not halt with any input (roughly, the set of programs non-halting with any input), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
    runmxx;
    accept;
}
```

### Exercise 5: $\neg K \leq\ \\{ p \mid \forall y:\ M\_p(y)=y \\}$

Reduce $\neg K$ to the set of natural numbers such that the program codified by them computes the identity function (roughly, the set of programs that compute the identity function), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
	if (mxxstopsininputsteps)
		output 1;
  
  	else output y;
}
```

_Note:_ $x \notin K \Rightarrow M_x(x)\ \uparrow \Rightarrow \forall y\ M_p(y) = y$ _where_ $p$ _is the program we just built. Then_ $x \in \\{p \mid \forall y\ M_p(y) = y\\}$.

### Exercise 6: $\neg K \leq\ \\{ p \mid \varphi_p\text{ total and injective} \\}$

Reduce $\neg K$ to the set of natural numbers such that the program codified by them computes some total and injective function (roughly, the set of programs that compute some total and injective function), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
	if (mxxstopsininputsteps)
		output 0; 
	else
		output y;
}
```

_Note: The identity function is total and injective_

### Exercise 8: $\neg K\ \leq\ \\{ p \mid M_p(1){\downarrow} \ \wedge\  M_p(2){\uparrow} \\}$

Reduce $\neg K$ K to the set of natural numbers such that the program codified by them halt with input 11 and do not halt with input 22 (roughly, the set of programs that halt with input 11 and do not halt with input 22), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
  	if (y == 1) accept;
  	
	runmxx;
  
  	accept;
  	
}
```

### Exercise 9: $K\ \leq\ \\{ p \mid |\mathtt{Dom}(\varphi_p)|\geq 2 \\}$

Reduce $K$ to the set of natural numbers codifying programs such that the domain of the function computed by the program has cardinal at least $2$ (roughly, the set of programs implementing functions whose domain has at least two elements) in order to prove that such set is undecidable (not recursive).

```c
input y
{
	runmxx;
  	output y;
}
```

_Note: If we are in a negative case and_ $M_x(x)$ _does not halt, then the domain will be zero since the program will not halt._