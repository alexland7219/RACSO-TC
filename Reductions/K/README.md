# Exercises on reductions of programs

## _RACSO exercises on K-Reductions_

### Exercise 1: $K\ \leq\ \\{ p \mid \exists y:\ M_p(y){\downarrow} \\}$

Reduce $K$ to the set of natural numbers codifying programs such that the program halts with some input (roughly, the set of programs that halt with some input), in order to prove that such set is undecidable (not recursive).

```c
input y
{
    runmxx;
    infiniteloop;
}
```

### Exercise 2: $\overline{K} \leq\ \\{ p \mid \forall y:\ M\_p(y){\downarrow} \\}$

Reduce $\overline(K)$ to the set of natural numbers such that the program codified by them halts with any input (roughly, the set of programs that halt with any input), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
    if (mxxstopsininputsteps)
        infiniteloopp;
    
    accept;
}
```

### Exercise 3: $\overline{K} \leq\ \\{ p \mid \exists y:\ M\_p(y){\uparrow} \\}$

Reduce $\overline(K)$ to the set of natural numbers such that the program codified by them does not halt with some input (roughly, the set of programs non-halting with some input), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
    runmxx;
    accept;
}
```

### Exercise 4: $\overline{K} \leq\ \\{ p \mid \forall y:\ M\_p(y){\uparrow} \\}$

Reduce $\overline(K)$ to the set of natural numbers such that the program codified by them does not halt with any input (roughly, the set of programs non-halting with any input), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
    runmxx;
    accept;
}
```

### Exercise 5: $\overline\\{K\\} \leq\ \\{ p \mid \forall y:\ M\_p(y)=y \\}$

```c
input y
{
	if (mxxstopsininputsteps)
		output 1;
  
  	else output y;
}
```

_Note:_ $x \notin K \Rightarrow M_x(x) \uparrow \Rightarrow \forall y M_p(y) = y$ _where_ $p$ _is the program we just built. Then_ $x \in \\{p \mid \forall y M_p(y) = y\\}$.