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

The previous DFA can be described with the basic format as follows:

<div align="center">

|  | a | b |  |
|---|---|---|---|
| q0 | q1 | q0 | |
| q1 | q1 | q1 | + |
</div>


Note that the alphabet symbols are _a_ and _b_, and the states are _q0_ and _q1_. Moreover, _q1_ is
an accepting state since it is marked with +, and _q0_ is implicitly assumed to be the starting
state since it is the first one to appear. Finally, note that this format is roughly equivalent
to the automaton’s transition matrix, where the columns are indexed by alphabet symbols
and the rows are indexed by states.

## _RACSO exercises on DFAs_

### Exercise 1: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid |w|_a\in\dot{2} \\}$

Describe the minimum DFA that recognizes the language of the words over $\\{a, \\}$ which have an even number of _a_'s.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **E** | O | E | + |
| **O** | E | O | |
</div>

_Note: E for 'even' and O for 'odd'._

### Exercise 2: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid |w|_a\in\dot{2}\wedge |w|_b\in\dot{2} \\}$ 

Describe the minimum DFA that recognizes the language of words over $\\{a, b\\}$ with an even number of _a_'s, and an even number of _b_'s.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **EE** | OE | EO | + |
| **EO** | OO | EE | |
| **OE** | EE | OO | |
| **OO** | EO | OE | |
</div>

### Exercise 3: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid |w|_a\notin\dot{2}\vee |w|_b\notin\dot{2} \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ with an odd number of _a_'s or an odd number of _b_'s.
<div align="center">

|  | a | b |  |
|---|---|---|---|
| **EE** | OE | EO | |
| **EO** | OO | EE | + |
| **OE** | EE | OO | + |
| **OO** | EO | OE | + |
</div>

### Exercise 4: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \exists x: w=xa \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ that end in _a_.

<div align="center">

| | a | b | |
|---|---|---|---|
| **N** | Y | N | |
| **Y** | Y | N | + |
</div>

### Exercise 5: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \exists x: w=xbba \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ ending with _bba_.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **N** | N | B | |
| **B** | N | BB | |
| **BB** | Y | BB | |
| **Y** | N | B | + |
</div>

