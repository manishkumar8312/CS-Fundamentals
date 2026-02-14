# Finite Automata

Finite Automata are **abstract mathematical models of computation** used to recognize **regular languages**. They form the foundation of **lexical analysis, pattern matching, compiler design**, and many areas of theoretical computer science.

---

## 1. Deterministic Finite Automata (DFA)

A **Deterministic Finite Automaton (DFA)** is a finite state machine where **for every state and input symbol, exactly one transition is defined**.

### Key Characteristics

* Deterministic behavior
* No ambiguity in transitions
* Exactly one active state at any time
* Used to recognize regular languages

---

## 2. Formal Definition of DFA

A DFA is formally defined as a **5-tuple**:

[
M = (Q, \Sigma, \delta, q_0, F)
]

Where:

* `Q` → Finite set of states
* `Σ` → Finite input alphabet
* `δ` → Transition function
  [
  \delta : Q \times \Sigma \rightarrow Q
  ]
* `q₀` → Initial state (`q₀ ∈ Q`)
* `F` → Set of accepting (final) states (`F ⊆ Q`)

---

## 3. Transition Functions and State Diagrams

### Transition Function

The transition function defines how the automaton moves between states on reading input symbols.

Example:

```
δ(q0, 0) = q1
δ(q1, 1) = q2
```

### State Diagram

* States are represented as circles
* Initial state has an incoming arrow
* Final states are double circles
* Transitions are labeled with input symbols

State diagrams provide a **visual representation** of DFA behavior.

---

## 4. Language Acceptance by DFA

A DFA **accepts a string** if:

* Starting from the initial state
* After processing the entire input string
* The automaton ends in a **final state**

### Language Accepted by DFA

The language of a DFA `M` is defined as:
[
L(M) = { w \in \Sigma^* \mid \delta^*(q_0, w) \in F }
]

Where `δ*` is the extended transition function.

---

## 5. Non-Deterministic Finite Automata (NFA)

A **Non-Deterministic Finite Automaton (NFA)** allows:

* Multiple transitions for the same state and input symbol
* Transitions without consuming input (ε-moves)

### Differences from DFA

* May have **zero, one, or multiple transitions**
* Multiple active states possible
* Easier to design than DFA

---

## 6. ε-NFA and ε-Closure

### ε-NFA

An ε-NFA allows transitions on **ε (empty string)**, meaning the automaton can change state **without reading any input**.

### ε-Closure

The **ε-closure** of a state `q` is the set of states reachable from `q` using only ε-transitions.

Formally:
[
\varepsilon\text{-closure}(q) = { p \mid p \text{ reachable from } q \text{ using ε-moves} }
]

ε-closure is essential for converting ε-NFA to DFA.

---

## 7. Equivalence of DFA, NFA, and ε-NFA

### Important Result

> **DFA, NFA, and ε-NFA recognize exactly the same class of languages — the regular languages.**

Key points:

* Every NFA can be converted to an equivalent DFA
* Every ε-NFA can be converted to an equivalent NFA
* NFAs do not increase expressive power, only convenience

---

## 8. Conversion of NFA to DFA (Subset Construction)

### Idea

Each DFA state represents a **set of NFA states**.

### Steps

1. Start state = ε-closure of NFA start state
2. For each DFA state and input symbol:

   * Compute reachable NFA states
   * Take ε-closure
3. Repeat until no new states are generated
4. Mark DFA final states (if any NFA final state is included)

### Note

* Resulting DFA may have up to (2^n) states
* Conversion is guaranteed to terminate

---

## 9. Minimization of DFA

### Objective

Reduce the number of states **without changing the language** accepted by the DFA.

### Why Minimize?

* Optimized memory usage
* Faster execution
* Simpler representation

### DFA Minimization Techniques

* Table-filling method
* Partitioning method

### Basic Idea

* Remove unreachable states
* Merge equivalent states (states that behave identically for all inputs)

---

## 10. Design of Finite Automata for Given Languages

### Common Design Strategies

* Start by identifying **patterns in strings**
* Use states to represent **progress in pattern matching**
* Handle repetitions using loops
* Carefully manage accepting states

### Examples of Languages

* Strings ending with `01`
* Strings with even number of `0`s
* Strings containing substring `aba`
* Binary strings divisible by 3

Designing automata improves:

* Pattern recognition skills
* Logical reasoning
* Problem-solving ability (important for GATE)

---

## Summary

* DFA is deterministic and strict
* NFA and ε-NFA are flexible and easier to design
* All finite automata models are **equivalent in power**
* Conversion and minimization are key exam topics
* Finite automata define **regular languages**

This chapter forms the **foundation of automata theory** and is heavily used in **pumping lemma, regular expressions, and compiler design**.

---

⭐ **Star the repository if you find it useful**

