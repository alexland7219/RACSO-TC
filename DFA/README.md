# Deterministic Finite Automaton
## _Basic format describing DFAs_

In order to describe a DFA we write its alphabet in the first line, and in each of the following
lines we define a state by giving the following information: (i) the state name, (ii) the state
reached after reading each alphabet symbol, in the order specified in the first line, and (iii)
a symbol + when the state is accepting. Note that there is no way for specifying the initial
state since, by default, it is the first one to appear.

In order to conclude, we give an illustrative example. Consider the minimum DFA
recognizing the language over the alphabet $\\{a, b \\}$ with at least one occurrence of $a$:


<p align="center">
<img src="https://i.imgur.com/xHMUuFS.png" alt="DFA Example">
</p>
_Image 1: DFA that recognizes the language_ $\\{ w \in \\{a,b \\}^* \mid |w|_a > 0 \\}$

The previous DFA can be described with the basic format as follows:

<div align="center">

|  | a | b |  |
|---|---|---|---|
| q0 | q1 | q0 | |
| q1 | q1 | q1 | + |
</div>
<br/>
Note that the alphabet symbols are _a_ and _b_, and the states are _q0_ and _q1_. Moreover, _q1_ is
an accepting state since it is marked with +, and _q0_ is implicitly assumed to be the starting
state since it is the first one to appear. Finally, note that this format is roughly equivalent
to the automaton’s transition matrix, where the columns are indexed by alphabet symbols
and the rows are indexed by states.
