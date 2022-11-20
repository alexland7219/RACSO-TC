# Exercises on reductions of programs

## _RACSO exercises on K-Reductions_

### Exercise 1: $K\ \leq\ \\{ p \mid \exists y:\ M_p(y){\downarrow} \\}$

Reduce $K$ to the set of natural numbers codifying programs such that the program halts with some input (roughly, the set of programs that halt with some input), in order to prove that such set is undecidable (not recursive).

```c
input y
{
    if (mxxstopsininputsteps)
        accept;
    infiniteloop;
}