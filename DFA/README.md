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


Note that the alphabet symbols are $a$ and $b$, and the states are $q0$ and $q1$. Moreover, $q1$ is
an accepting state since it is marked with +, and $q0$ is implicitly assumed to be the starting
state since it is the first one to appear. Finally, note that this format is roughly equivalent
to the automaton’s transition matrix, where the columns are indexed by alphabet symbols
and the rows are indexed by states.

## _RACSO exercises on DFAs_

### Exercise 1: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid |w|_a\in\dot{2} \\}$

Describe the minimum DFA that recognizes the language of the words over $\\{a, b\\}$ which have an even number of $a$'s.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **E** | O | E | + |
| **O** | E | O | |
</div>

_Note: E for 'even' and O for 'odd'._

### Exercise 2: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid |w|_a\in\dot{2}\wedge |w|_b\in\dot{2} \\}$ 

Describe the minimum DFA that recognizes the language of words over $\\{a, b\\}$ with an even number of $a$'s, and an even number of $b$'s.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **EE** | OE | EO | + |
| **EO** | OO | EE | |
| **OE** | EE | OO | |
| **OO** | EO | OE | |
</div>

### Exercise 3: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid |w|_a\notin\dot{2}\vee |w|_b\notin\dot{2} \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ with an odd number of $a$'s or an odd number of $b$'s.
<div align="center">

|  | a | b |  |
|---|---|---|---|
| **EE** | OE | EO | |
| **EO** | OO | EE | + |
| **OE** | EE | OO | + |
| **OO** | EO | OE | + |
</div>

_Note: This exercise is the exact opposite of the previous one. To negate a DFA we just toggle the acceptance of all states.
This is exactly why languages recognized by DFAs, regular languages, are closed under complement_

### Exercise 4: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \exists x: w=xa \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ that end in $a$.

<div align="center">

| | a | b | |
|---|---|---|---|
| **N** | Y | N | |
| **Y** | Y | N | + |
</div>

### Exercise 5: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \exists x: w=xbba \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ ending with $bba$.

<div align="center">

|  | a | b |  |
|---|---|---|---|
| **N** | N | B | |
| **B** | N | BB | |
| **BB** | Y | BB | |
| **Y** | N | B | + |
</div>

### Exercise 6: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \exists x: w=xbabab \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ ending with $babab$.

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

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ such that the symbol $a$ appears in the third from the last position, and the symbol $b$ appears in the penultimate position.

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

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ such that to the left of each occurrence of $a$ there is an even number of $b$'s.

<div align="center">

|  | a | b | |
|---|---|---|---|
| **A** | A | B | + |
| **B** | W | A | + |
| **W** | W | W | |
</div>

_Note: This is our first introduction to our "**W**ell" state. We start reading the word until we find one _a_ with an odd number of _b_'s to its left. In that case we don't care about the rest of the word anymore. From the **W**ell you may never escape._

### Exercise 9: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \forall x,y: (w=xay \Rightarrow |y|_b\in\dot{2}) \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ such that to the right of each occurrence of $a$ there is an even number of $b$'s.

<div align="center">

|  | a | b | |
|---|---|---|---|
| **S** | A | S | + |
| **A** | A | C | + |
| **C** | W | A | |
| **W** | W | W | |
</div>

### Exercise 10: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \forall x,y: ( (w=xy \wedge |x|\geq 3) \Rightarrow (|x|_a\in\dot{2}\vee |x|_b\in\dot{2}) ) \\}$

Describe the minimum DFA that recognizes the language of the words over $\\{a, b\\}$ such that every prefix of length greater than or equal to $3$ has an even number of $a$'s or an even number of $b$'s.

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

Describe the minimum DFA that recognizes the language of the words over $\\{a, b\\}$ such that every prefix of length greater than or equal to $3$ has an even number of $a$'s or an odd number of $b$'s.

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

Describe the minimum DFA that recognizes the language of the words over $\\{a, b\\}$ whose subwords of length $3$ have an even number of $a$'s or an odd number of $b$'s.

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

### Exercise 13: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \forall x,y,z: ( (w=xyz \wedge |y|=3) \Rightarrow (|y|_a\in\dot{2} \vee |y|_b\in\dot{2}) ) \\}$
  
Describe the minimum DFA that recognizes the language of the words over $\\{a, b\\}$ whose subwords of length $3$ have an even number of $a$'s or an even number of $b$'s.

<div align="center">

| | a | b | |
|---|---|---|---|
| **T** | T | T | + |
</div>

_Note: If you really think about it, any word of length 3 over \{a, b\} will always have either an even number of a's or of b's_

### Exercise 14: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid \forall x: (w=bbx \Rightarrow |x|_{aa}=0) \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ such that, if they start with $bb$, then they do not contain $aa$.

<div align="center">

| | a | b | |
|---|---|---|---|
| **S** | Y | B | + |
| **B** | Y | C | + |
| **C** | D | C | + |
| **D** | W | C | + |
| **Y** | Y | Y | + |
| **W** | W | W | |
</div>

_Note: In this case we combine a **W**ell with a special state, we will call the **Y**es state. Once we are in **Y** the word will always be accepted. Any word starting with ab will be accepted, for example._

### Exercise 15: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid |w|_{bbb}=0 \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ that do not contain the subword $bbb$.

<div align="center">

| | a | b | |
|---|---|---|---|
| **0** | 0 | 1 | + |
| **1** | 0 | 2 | + |
| **2** | 0 | W | + |
| **W** | W | W | |
</div>

### Exercise 16: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid |w|_{bab}=0 \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ that do not contain the subword $bab$.

<div align="center">

| | a | b | |
|---|---|---|---|
| **S** | S | A | + |
| **A** | B | A | + |
| **B** | S | W | + |
| **W** | W | W | |
</div>

### Exercise 17: Minimum DFA for $\\{ w \in \\{a,b\\}^* \mid |w|\_{aba}=0 \wedge |w|\_{bab}=0 \wedge \exists x: w=xaaa \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ that end in $aaa$, and do not contain $aba$ or $bab$.

<div align="center">

| | a | b | |
|---|---|---|---|
| **S** | A | B | |
| **A** | C | D | |
| **B** | F | B | |
| **C** | G | D | |
| **D** | W | B | |
| **F** | C | W | |
| **G** | G | D | + |
| **W** | W | W | |
</div>

### Exercise 18: Minimum DFA for $\\{ w \in \\{a,b,c\\}^* \mid |w|_{abc}\leq 1 \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ that have at most one occurrence of the subword $abc$.

<div align="center">

| | a | b | c | |
|---|---|---|---|---|
| **S** | A1 | S | S | + |
| **A1** | A1 | AB1 | S | + |
| **AB1** | A1 | S | C | + |
| **C** | A2 | C | C | + |
| **A2** | A2 | AB2 | C | + |
| **AB2** | A2 | C | W | + |
| **W** | W | W | W | |
</div>

_Note: Just after reading the first abc we always go to state **C**. Afterwards if we were to read another abc we would go to **W**._

### Exercise 19: Minimum DFA for $\\{ w \in \\{a,b,c\\}^* \mid \forall x,y,z: (w=xbybz \Rightarrow |y|_a\geq 2) \\}$

Describe the minimum DFA that recognizes the words over $\\{a, b\\}$ such that between every two occurrences of $b$ there are at least two occurrences of $a$.

<div align="center">

| | a | b | c | |
|---|---|---|---|---|
| **S** | S | F | S | + |
| **F** | 1 | W | F | + |
| **1** | S | W | 1 | + |
| **W** | W | W | W | |
</div>

### Exercise 20: Minimum DFA for $\\{ w \in \\{0,1\\}^* \mid \mathtt{value}_2(w)\in\dot{2} \\}$

Describe the minimum DFA that recognizes the words over $\\{0, 1\\}$ such that interpreted in binary represent a natural number multiple of $2$ (in particular, the empty word represents $0$, which is multiple of $2$).

<div align="center">

| | 0 | 1 | |
|---|---|---|---|
| **Y** | Y | N | + |
| **N** | Y | N | |
</div>

_Note: Now our alphabet is_ $\Sigma=\\{0, 1\\}$ _and words are binary numbers. In binary, multiples of_ $2$ _are those that end in a_ $0$

### Exercise 21: Minimum DFA for $\\{ w \in \\{0,1\\}^* \mid \mathtt{value}_2(w)\in\dot{3} \\}$

Describe the minimum DFA that recognizes the words over $\\{0, 1\\}$ such that interpreted in binary represent a natural number multiple of $3$ (in particular, the empty word represents $0$, which is multiple of $3$).

<div align="center">

| | 0 | 1 | |
|---|---|---|---|
| **M0** | M0 | M1 | + |
| **M1** | M2 | M0 | |
| **M2** | M1 | M2 | |
</div>

_Note: Consider three states for the remainder of the word modulus_ $3$ _. Adding a_ $0$ _is equivalent to multiplying by two, and adding a_ $1$ _means multiplying by two then adding one_

### Exercise 22: Minimum DFA for $\\{ w \in \\{0,1\\}^* \mid \mathtt{value}_2(w)\notin\dot{3} \\}$

Describe the minimum DFA that recognizes the words over $\\{0, 1\\}$ such that interpreted in binary represent a natural number which is not multiple of $3$ (in particular, the empty word represents $0$, which is multiple of $3$).

<div align="center">

| | 0 | 1 | |
|---|---|---|---|
| **M0** | M0 | M1 | |
| **M1** | M2 | M0 | + |
| **M2** | M1 | M2 | + |
</div>

### Exercise 23: Minimum DFA for $\\{ w \in \\{0,1\\}^* \mid \mathtt{value}_2(w)\in\dot{4} \\}$

Describe the minimum DFA that recognizes the words over $\\{0, 1\\}$ such that interpreted in binary represent a natural number multiple of $4$ (in particular, the empty word represents $0$, which is multiple of $4$).

<div align="center"

| | 0 | 1 | |
|---|---|---|---|
| **Y** | Y | N | + |
| **N** | F | N | |
| **F** | Y | N | |
</div>

_Note: In binary, multiples of_ $4$ _are those that end in two zeros_
