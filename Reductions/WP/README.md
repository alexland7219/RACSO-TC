# Exercises on reductions of programs

## _RACSO exercises on Word Reachability reductions_

### Exercise 1: $\\{\langle u,v,R\rangle\mid\Sigma=\\{a,b\\}\ \wedge\ u\to\_R^\*v\\}\quad\leq\quad\\{\langle u,v,R\rangle \mid |\Sigma|\leq 2\ \wedge\ u\to\_R^\*v\ \wedge\ |R|\in\dot\\{2\\}\text\\{ (as a list, i.e., counting repetitions)\\}\\}$

Reduce the word reachability problem restricted to the alphabet $\\{a,b\\}$ to the set of tuples $\langle u,v,R\rangle$ where $u,v$ are words, $R$ is a word rewrite system, the used alphabet has at most $2$ symbols, $u$ reaches $v$ using $R$, and the number of rules of $R$ is even (by considering $R$ as a list, i.e., each different rule is counted as many times as it occurs in $R$), in order to prove that such set is undecidable (not recursive). 

```rust
u
v
l->r
l->r
```

_Note: Allowing repetitions, we just duplicate R_

