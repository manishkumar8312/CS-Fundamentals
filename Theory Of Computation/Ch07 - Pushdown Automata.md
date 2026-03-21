# Pushdown Automata (PDA)

## 1. Introduction

A Pushdown Automaton (PDA) is a computational model that extends a Finite Automaton by incorporating an auxiliary memory structure called a **stack**. This additional memory enables PDAs to recognize a broader class of languages known as **Context-Free Languages (CFLs)**.

PDAs are widely used in parsing, compiler design, and formal language theory.

---

## 2. Formal Definition

A Pushdown Automaton is formally defined as a 7-tuple:

M = **Q**, **Σ (Sigma)**, **Γ (Gamma)**, **δ (Delta)**, **q₀**, **Z₀**, **F**

### Components:

* **Q**: Finite set of states
* **Σ (Sigma)**: Input alphabet
* **Γ (Gamma)**: Stack alphabet
* **δ (Delta)**: Transition function
* **q₀**: Initial state, where ( q_0 \in Q )
* **Z₀**: Initial stack symbol, where ( Z_0 \in \Gamma )
* **F**: Set of final (accepting) states, where ( F \subseteq Q )

---

## 3. Transition Function

The transition function defines the behavior of the PDA:

`δ(q, a, X) = (p, γ)`

### Interpretation:

* The PDA is in state ( q )
* It reads input symbol ( a ) (or ε for no input)
* The top of the stack is ( X )
* It moves to state ( p )
* It replaces ( X ) with string ( \gamma ) on the stack

This operation may correspond to:

* **Push** (if `γ` adds symbols)
* **Pop** (if `γ = ε`)
* **Replace** (if `γ` modifies the top symbol)

---

## 4. Stack Operations

The stack is a Last-In-First-Out (LIFO) data structure and is central to the functioning of a PDA.

### Basic Operations:

* **Push**: Add one or more symbols to the stack
* **Pop**: Remove the top symbol from the stack
* **No operation (ε-transition)**: Perform a transition without modifying the stack

The stack enables the PDA to keep track of nested structures such as parentheses, making it suitable for context-free languages.

---

## 5. Acceptance by Empty Stack

A PDA is said to accept a string by **empty stack** if:

* After consuming the entire input string
* The stack becomes empty

### Key Characteristics:

* Acceptance does not depend on reaching a final state
* The input is accepted solely based on stack emptiness

---

## 6. Acceptance by Final State

A PDA is said to accept a string by **final state** if:

* After consuming the entire input string
* The PDA reaches a state in the set ( F )

### Key Characteristics:

* The stack may or may not be empty
* Acceptance depends on reaching a designated final state

---

## 7. Equivalence of Acceptance Methods

The two acceptance methods are equivalent in terms of computational power:

* Every PDA that accepts by empty stack can be converted to one that accepts by final state
* Every PDA that accepts by final state can be converted to one that accepts by empty stack

Thus, both methods recognize exactly the class of **Context-Free Languages (CFLs)**.

---

## 8. Equivalence of PDA and CFG

Pushdown Automata and Context-Free Grammars are equivalent in expressive power:

* For every **Context-Free Grammar (CFG)**, there exists an equivalent **PDA**
* For every **PDA**, there exists an equivalent **CFG**

### Implication:

Both models define the same class of languages, i.e., Context-Free Languages.

---

## 9. Construction of PDA for Given Languages

Constructing a PDA typically involves designing stack operations to track patterns in the input.

### General Strategy:

1. **Identify the structure of the language**
   Example: ( a^n b^n ), balanced parentheses, palindromes

2. **Use the stack to store information**

   * Push symbols while reading the first part of the input
   * Pop symbols while matching the second part

3. **Define transitions carefully**

   * Handle input symbols and stack symbols simultaneously
   * Use ε-transitions where necessary

---
### Example: PDA for Language `L = { a^n b^n | n ≥ 0 }`

#### Idea:

* Push one symbol onto the stack for each ( a )
* Pop one symbol for each ( b )
* Accept when all symbols are matched

#### Transitions:
* `δ(q₀, a, Z₀) = (q₀, aZ₀)`
* `δ(q₀, a, a)  = (q₀, aa)`
* `δ(q₀, b, a)  = (q₁, ε)`

Acceptance can be defined either:

* By empty stack, or
* By reaching a final state after stack operations

---

## 10. Conclusion

Pushdown Automata play a fundamental role in theoretical computer science by enabling the recognition of context-free languages. The introduction of a stack allows PDAs to handle nested and recursive structures, making them significantly more powerful than finite automata.

Their equivalence with context-free grammars establishes a strong theoretical foundation for applications such as syntax analysis and compiler design.

