# Introduction to Theory of Computation

Theory of Computation (TOC) is a foundational subject in computer science that studies **abstract models of computation**, **formal languages**, and **the limits of what can be computed**. It provides a mathematical framework to analyze problems independent of programming languages or hardware.

---

## 1. What is Theory of Computation?

Theory of Computation answers three fundamental questions:

1. **What problems can be solved using algorithms?**
2. **How efficiently can these problems be solved?**
3. **What problems cannot be solved at all?**

TOC forms the theoretical basis for:

* Automata theory
* Compiler design
* Algorithm analysis
* Artificial intelligence
* Complexity theory

---

## 2. Motivation and Applications of TOC

### Why Study TOC?

* To understand the **capabilities and limitations of computers**
* To formally reason about **program behavior**
* To design **efficient algorithms**
* To identify **unsolvable problems**

### Applications

* **Compiler design** (lexical analysis, parsing)
* **Pattern matching** and text processing
* **Formal verification** of systems
* **Natural language processing**
* **Complexity analysis** of algorithms

---

## 3. Alphabets, Strings, and Languages

### Alphabet (Σ)

An **alphabet** is a finite, non-empty set of symbols.

Example:

```
Σ = {0, 1}
Σ = {a, b, c}
```

---

### String

A **string** is a finite sequence of symbols from an alphabet.

Example:

```
If Σ = {a, b}
Strings: a, ab, bba, ε
```

* **ε (epsilon)** represents the empty string
* Length of a string `w` is denoted by `|w|`

---

### Language

A **language** is a set of strings formed over an alphabet.

Example:

```
L = {ε, a, ab, abb}
```

Languages are the main objects studied in TOC.

---

## 4. Operations on Strings

Let `x` and `y` be two strings.

### Concatenation

Joining two strings.

```
x = ab
y = ba
x · y = abba
```

---

### Length

Number of symbols in a string.

```
|abba| = 4
|ε| = 0
```

---

### Reverse

Reversing the order of symbols.

```
reverse(abc) = cba
```

---

## 5. Operations on Languages

Let `L1` and `L2` be languages.

### Union

```
L1 ∪ L2 = { w | w ∈ L1 or w ∈ L2 }
```

---

### Intersection

```
L1 ∩ L2 = { w | w ∈ L1 and w ∈ L2 }
```

---

### Difference

```
L1 − L2 = { w | w ∈ L1 and w ∉ L2 }
```

---

### Concatenation

```
L1L2 = { xy | x ∈ L1 and y ∈ L2 }
```

---

### Complement

```
L̅ = Σ* − L
```

---

## 6. Kleene Star and Positive Closure

### Kleene Star (L*)

Represents **zero or more repetitions** of strings from a language.

```
L* = { ε, L, LL, LLL, ... }
```

Example:

```
If L = {a}
L* = {ε, a, aa, aaa, ...}
```

---

### Positive Closure (L⁺)

Represents **one or more repetitions** of strings from a language.

```
L⁺ = { L, LL, LLL, ... }
```

Relationship:

```
L* = L⁺ ∪ {ε}
```

---

## 7. Homomorphism and Inverse Homomorphism

### Homomorphism

A **homomorphism** is a function that maps symbols of one alphabet to strings of another alphabet.

Example:

```
h(a) = 01
h(b) = 10
```

For string `ab`:

```
h(ab) = h(a)h(b) = 0110
```

---

### Inverse Homomorphism

Given a homomorphism `h`, the **inverse homomorphism** of a language `L` is:

```
h⁻¹(L) = { w | h(w) ∈ L }
```

It is used to analyze **language transformations** and closure properties.

---

## Summary

* TOC studies **computation, languages, and limits of algorithms**
* Alphabets → Strings → Languages form the basic hierarchy
* String and language operations help define language behavior
* Kleene star and closure define repetition
* Homomorphisms transform languages formally

This chapter builds the **foundation for automata, grammars, and Turing machines**.

---

⭐ **Star the repository if you find it useful**
