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

### Exercise 7: $\neg K\ \leq\ \\{ p \mid \varphi_p\text{ total and non-injective} \\}$

Reduce $\neg K$ to the set of natural numbers such that the program codified by them computes some total and non-injective function (roughly, the set of programs that compute some total and non-injective function), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y {
	if (not mxxstopsininputsteps) output 0;
	else infiniteloop;
}
```

### Exercise 8: $\neg K\ \leq\ \\{ p \mid M_p(1){\downarrow} \ \wedge\  M_p(2){\uparrow} \\}$

Reduce $\neg K$ K to the set of natural numbers such that the program codified by them halt with input $1$ and do not halt with input $2$ (roughly, the set of programs that halt with input $1$ and do not halt with input $2$), in order to prove that such set is not semi-decidable (not recursively enumerable).

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

### Exercise 10: $\neg K\ \leq\ \\{ p \mid |\mathtt{Dom}(\varphi_p)|=2 \\}$

Reduce $\neg K$ to the set of natural numbers codifying programs such that the domain of the function computed by the program has cardinal $2$ (roughly, the set of programs implementing functions whose domain has exactly two elements) in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
  	if (not mxxstopsininputsteps){
  		if (y == 0 or y == 1) accept;
	  	else reject;
	}
  	else accept;
}
```

### Exercise 11: $K\ \leq\ \\{ p \mid |\mathtt{Im}(\varphi_p)|\geq 2 \\}$

Reduce $K$ to the set of natural numbers codifying programs such that the image of the function computed by the program has cardinal at least $2$ (roughly, the set of programs implementing functions whose image has at least two elements) in order to prove that such set is undecidable (not recursive).

```c
input y
{
	runmxx;
  	
  	output (y % 2);
}
```

### Exercise 12: $\neg K\ \leq\ \\{ p \mid |\mathtt{Im}(\varphi_p)|=2 \\}$

Reduce $\neg K$ to the set of natural numbers codifying programs such that the image of the function computed by the program has cardinal $2$ (roughly, the set of programs implementing functions whose image has exactly two elements) in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
	if (not mxxstopsininputsteps) output (y % 2);
  	else output y;
}
```

### Exercise 13: $\neg K\ \leq\ \\{ p \mid |\mathtt{Dom}(\varphi_p)|=\infty\ \wedge\ |\mathtt{Im}(\varphi_p)|=\infty\ \wedge\ \mathtt{Dom}(\varphi_p)\cap\mathtt{Im}(\varphi_p)=\emptyset \\}$

Reduce $K$ to the set of natural numbers codifying programs such that the domain and the image of the function computed by the program have infinite cardinal and are disjoint (roughly, the set of programs implementing functions whose domain and image are infinite and disjoint) in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
 	if (not mxxstopsininputsteps){
		if (y % 2) output y + 1;
	  	else reject;
  	}
  	else reject;
}
```

_Note: In this case the domain are the even numbers and the image the odd numbers. Both sets are disjoint, and will be infinite if the machine never halts for any y. If it were to halt after some y, then we would only reject and never reach infinity_

### Exercise 14: $K\ \leq\ \\{ \langle p,q\rangle \mid \exists y:\ (M_p(y){\downarrow} \ \wedge\  M_q(y){\downarrow}) \\}$

Reduce $K$ to the set of pairs of natural numbers codifying programs halting with a common input (roughly, the set of pairs of programs which stop with the same common input), in order to prove that such set is undecidable (not recursive).

```c
input y
{
	runmxx;
  	accept;
}

input y
{
	runmxx;
  	accept;
}
```

### Exercise 15: $\neg K \leq \\{\langle p, q \rangle \mid \exists y : (M_p(y)\downarrow \wedge\ M_q(y)\uparrow)\\}$

Reduce $\neg K$ to the set of pairs of natural numbers codifying programs such that there exists an input for which the first program halts and the second program does not halt (roughly, the set of pairs of programs which stop and do not stop with some common input), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
	if (mxxstopsininputsteps)
		infiniteloop;
 	else accept;
}

input y
{_
	runmxx;
  	accept;
}
```

### Exercise 16: $\neg K \leq \\{\langle p, q \rangle \mid \exists y_1, y_2 : (M_p(y_1)\downarrow \wedge\ M_q(y_1)\uparrow \wedge\ M_p(y_2)\uparrow \wedge\ M_q(y_2)\downarrow)\\}$

Reduce $\neg K$ to the set of pairs of natural numbers codifying programs such that there exists an input for which the first program halts and the second program does not halt, and there exists an input for which the first program does not halt and the second program halts, (roughly, the set of pairs of programs which stop and do not stop with some common input, and do not stop and stop with some other common input), in order to prove that such set is not semi-decidable (not recursively enumerable).


```c
input y
{
	if (y == 0) accept;
  	
  	runmxx;
  
  	accept;
}	

input y
{
	if (y == 0) infiniteloop;
  	else accept;
}
```

### Exercise 17: $K \leq \\{\langle p, q \rangle \mid | \mathtt{Dom}(\varphi_p)\cap\mathtt{Dom}(\varphi_q)| \ge 2\\}$

Reduce $K$ to the set of pairs of natural numbers codifying programs such that the domains of the functions implemented by them share at least two elements (roughly, the set of pairs of programs implementing functions whose domains share at least two elements), in order to prove that such set is undecidable (not recursive).

```c
input y
{
	runmxx;
  	accept;
}

input y
{
	runmxx;
  	accept;
}
```

### Exercise 18: $\neg K \leq \\{\langle p, q \rangle \mid | \mathtt{Dom}(\varphi_p)\cap\mathtt{Dom}(\varphi_q)| = 2\\}$

Reduce $\neg K$ to the set of pairs of natural numbers codifying programs such that the domains of the functions implemented by them share exactly two elements (roughly, the set of pairs of programs implementing functions whose domains share exactly two elements), in order to prove that such set is not semi-decidable (not recursively enumerable).

```c
input y
{
	if (not mxxstopsininputsteps)
	  	if (y < 2) accept;
  		else reject;
 	else accept;
}

input y
{
	if (not mxxstopsininputsteps)
	  	if (y < 2) accept;
  		else reject;
 	else accept;
}
```

### Exercise 19: $\neg K \leq \\{\langle p, q \rangle \mid | \mathtt{Dom}(\varphi_p) | = | \mathtt{Dom}(\varphi_q) | = | \mathtt{Im1}(\varphi_p) | = | \mathtt{Im}(\varphi_q) | \wedge | \mathtt{Dom}(\varphi_p) \cup \mathtt{Dom}(\varphi_q) \cup  \mathtt{Im}(\varphi_p) \cup  \mathtt{Im1}(\varphi_q) | = 1\\}$

Reduce $\neg K$ to the set of pairs of natural numbers codifying programs such that each domain and image of the function computed by each of such programs has exactly $1$ element, and the union of the domains and images of both programs has exactly $1$ element (roughly, the set of pairs of programs whose domains and images have exactly $1$ element, and the union of all such domains and images have exactly $1$ element) in order to prove that such set is not semi-decidable (not recursively enumerable).


```c
input y
{
	if (not mxxstopsininputsteps)
		if (y == 1) output 1;
  		else reject;
	else accept;
}

input y
{
  	if (not mxxstopsininputsteps)
		if (y == 1) output 1;
  		else reject;
 	else accept;
}
```
