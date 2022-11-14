# Deterministic Finite Automaton (Autòmat Finit Determinista)
## _Basic format describing DFAs_

In order to describe a DFA we write its alphabet in the first line, and in each of the following
lines we define a state by giving the following information: (i) the state name, (ii) the state
reached after reading each alphabet symbol, in the order specified in the first line, and (iii)
a symbol + when the state is accepting. Note that there is no way for specifying the initial
state since, by default, it is the first one to appear.

In order to conclude, we give an illustrative example. Consider the minimum DFA
recognizing the language over the alphabet $\\{a, b \\}$ with at least one occurrence of $a$:

![DFA Example](https://i.imgur.com/xHMUuFS.png)

_Image 1: DFA that recognizes the language $\\{ w \in \\{a,b \\}^* \mid |w|\_a\ge 0 \\}$_
The previous DFA can be described with the basic format as follows:

| Q | a | b | ? |
|---|---|---|---|
| q0 | q1 | q0 | |
| q1 | q1 | q1 | + |

