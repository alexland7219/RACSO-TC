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

Describe the minimum DFA that recognizes the language of the words over $\\{a, b\\}$ which have an even number of _a_'s.

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

### Exercise 6: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \exists x: w=xbabab \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ ending with _babab_.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **N** | N | B | |
| **B** | A | B | |
| **A** | N | D | |
| **D** | C | B | |
| **C** | N | Y | |
| **Y** | C | B | + | 
</div>

_Note: Always ask yourself in which state we end up if the word breaks the sequence babab at some state._

### Exercise 7: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \exists x,y: (w=xaby \wedge |y|=1) \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ such that the symbol _a_ appears in the third from the last position, and the symbol _b_ appears in the penultimate position.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **S** | A | S | |
| **A** | A | B | |
| **B** | C | D | |
| **C** | A | B | + |
| **D** | A | S | + |
</div>

### Exercise 8: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \forall x,y: (w=xay \Rightarrow |x|_b\in\dot{2}) \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ such that to the left of each occurrence of _a_ there is an even number of _b_'s.

<div align="center">

|  | a | b | |
|---|---|---|---|
| **A** | A | B | + |
| **B** | W | A | + |
| **W** | W | W | |
</div>

_Note: This is our first introduction to our "**W**ell" state. We start reading the word until we find one _a_ with an odd number of _b_'s to its left. In that case we don't care about the rest of the word anymore. From the **W**ell you may never escape._

### Exercise 9: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \forall x,y: (w=xay \Rightarrow |y|_b\in\dot{2}) \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ such that to the right of each occurrence of _a_ there is an even number of _b_'s.

<div align="center">

|  | a | b | |
|---|---|---|---|
| **S** | A | S | + |
| **A** | A | C | + |
| **C** | W | A | |
| **W** | W | W | |
</div>

### Exercise 10: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \forall x,y: ( (w=xy \wedge |x|\geq 3) \Rightarrow (|x|_a\in\dot{2}\vee |x|_b\in\dot{2}) ) \\}$

Describe the minimum DFA that recognizes the language of the words over $\\{a, b\\}$ such that every prefix of length greater than or equal to $3$ has an even number of _a_'s or an even number of _b_'s.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **A** | C | B | + |
| **B** | D | E | + |
| **C** | E | D | + |
| **D** | G | H | + |
| **E** | H | G | + |
| **G** | W | E | + |
| **H** | E | W | + |
| **W** | W | W | |
</div>

### Exercise 11: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \forall x,y: ( (w=xy \wedge |x|\geq 3) \Rightarrow (|x|_a\in\dot{2}\vee |x|_b\notin\dot{2}) ) \\}$

Describe the minimum DFA that recognizes the language of the words over $\\{a, b\\}$ such that every prefix of length greater than or equal to $3$ has an even number of _a_'s or an odd number of _b_'s.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **A** | C | B | + |
| **B** | D | E | + |
| **C** | E | D | + |
| **D** | B | W | + |
| **E** | W | B | + |
| **W** | W | W | |
</div>

### Exercise 12: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \forall x,y,z: ( (w=xyz \wedge |y|=3) \Rightarrow (|y|_a\in\dot{2} \vee |y|_b\notin\dot{2}) ) \\}$

Describe the minimum DFA that recognizes the language of the words over $\\{a, b\\}$ whose subwords of length $3$ have an even number of _a_'s or an odd number of _b_'s.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **S** | A | B | + |
| **A** | X | Z | + |
| **B** | U | Y | + |
| **X** | W | Z | + |
| **Y** | W | Y | + |
| **Z** | U | W | + |
| **U** | X | W | + |
| **W** | W | W | |
</div>

_Note: This exercise follows the trend of the previous ones. Now we have to keep track of our past two symbols in order to determine if we fall in the **W**ell._
