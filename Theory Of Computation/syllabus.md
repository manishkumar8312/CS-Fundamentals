# 📘 THEORY OF COMPUTATION – Syllabus

## Chapter 1. Introduction to Theory of Computation

- What is Theory of Computation? (Automata, Computability, Complexity)
- Motivation and applications: compilers, software verification, artificial intelligence, cryptography
- Alphabets, strings, and languages – basic definitions
- Operations on strings: concatenation, reversal, substring, length
- Operations on languages: union, intersection, concatenation, complement, Kleene star, positive closure
- Homomorphism and inverse homomorphism

---

## Chapter 2. Finite Automata

- Deterministic Finite Automata (DFA)
  - Formal definition (5‑tuple)
  - Transition functions and state diagrams
  - Language acceptance by DFA
- Non‑Deterministic Finite Automata (NFA)
  - Definition and why non‑determinism is useful
  - ε‑NFA and ε‑closure
- Equivalence of DFA, NFA, and ε‑NFA (proof outline)
- Conversion of NFA to DFA (subset construction)
- DFA Minimization – Table‑filling algorithm (Hopcroft’s algorithm) & Myhill–Nerode theorem
- Design of finite automata for given languages

---

## Chapter 3. Regular Languages and Regular Expressions

- Regular languages and their properties
- Regular expressions: syntax and semantics (ε, ∅, a, R1|R2, R1·R2, R*)
- Conversion of regular expressions to finite automata (Thompson’s construction)
- Conversion of finite automata to regular expressions (state elimination, Arden’s theorem)
- Closure properties of regular languages (union, intersection, complement, concatenation, Kleene star, reversal, homomorphism)
- Decision properties: emptiness, finiteness, membership, equivalence

---

## Chapter 4. Pumping Lemma for Regular Languages

- Statement of the pumping lemma
- Proof idea (pigeonhole principle on DFA states)
- Application of pumping lemma – proving a language is **not regular**
- Techniques for non‑regularity proofs (pumping, closure properties, Myhill–Nerode)
- Limitations of pumping lemma

---

## Chapter 5. Context‑Free Grammars (CFG)

- Context‑free grammars – components (V, Σ, R, S)
- Derivations and sentential forms
- Leftmost and rightmost derivations
- Parse trees
- Ambiguity in context‑free grammars (removing ambiguity where possible)
- Inherently ambiguous languages

---

## Chapter 6. Simplification and Normal Forms of CFG

- Removal of ε‑productions (nullable symbols)
- Removal of unit productions
- Removal of useless symbols (non‑generating, non‑reachable)
- Chomsky Normal Form (CNF) – definition and conversion algorithm
- Greibach Normal Form (GNF) – definition and conversion (conceptual)
- Conversion of any CFG to CNF (step‑by‑step)

---

## Chapter 7. Pushdown Automata (PDA)

- Definition and components of PDA (7‑tuple)
- Stack operations and instantaneous descriptions (ID)
- Acceptance by **empty stack** vs **final state** – equivalence
- Equivalence of PDA and CFG:
  - CFG → PDA (single‑state construction)
  - PDA → CFG (from empty‑stack acceptance)
- Construction of PDA for given languages

---

## Chapter 8. Pumping Lemma for Context‑Free Languages

- Statement of pumping lemma for CFL (based on parse tree height)
- Applications – proving languages are **not context‑free**
- Limitations of CFL pumping lemma (Ogden’s lemma mentioned)

---

## Chapter 9. Turing Machines

- Definition and components of a Turing Machine (7‑tuple: Q, Σ, Γ, δ, q₀, q_accept, q_reject)
- Instantaneous descriptions (ID) and how a TM computes
- Language acceptance by Turing Machine (halting in accept state)
- Design of Turing Machines for simple languages
- Variants of Turing Machines:
  - Multi‑tape Turing Machine (equivalent to single tape)
  - Non‑Deterministic Turing Machine (equivalent)
  - Multi‑head, two‑dimensional tapes (brief)
- Church–Turing thesis

---

## Chapter 10. Decidability and Undecidability

- Recursive (decidable) vs Recursively enumerable (r.e.) languages
- Decidable languages – membership can be decided by a TM that always halts
- Undecidable languages – no TM decides membership
- Halting problem – statement and proof of undecidability (diagonalisation)
- Reductions and reduction techniques (many‑one / mapping reductions)
- Rice’s Theorem – any non‑trivial property of r.e. languages is undecidable
- Proofs of undecidability for emptiness, regularity, and Post Correspondence Problem (PCP)

---

## Chapter 11. Chomsky Hierarchy

- Type‑0: Recursively Enumerable Languages (Turing machines)
- Type‑1: Context‑Sensitive Languages (Linear Bounded Automata – LBA)
  - Definition of LBA (Turing machine with bounded tape)
  - Example: `{aⁿbⁿcⁿ | n≥0}` is context‑sensitive
- Type‑2: Context‑Free Languages (Pushdown automata)
- Type‑3: Regular Languages (Finite automata)
- Relationships among language classes (proper inclusions: Regular ⊂ CFL ⊂ CSL ⊂ Recursive ⊂ RE)
- Closure and decision properties across the hierarchy

---

## Chapter 12. Introduction to Computational Complexity

- Time complexity – worst‑case number of steps
- Space complexity – worst‑case number of tape cells used
- Asymptotic notations (Big‑O, Big‑Ω, Big‑Θ) applied to TM resources
- Complexity classes:
  - P (polynomial time)
  - NP (nondeterministic polynomial time)
  - NP‑Hard and NP‑Complete (introductory level)
  - Brief mention of PSPACE, L, NL
- Polynomial‑time reductions (≤_p)
- Cook–Levin theorem (SAT is NP‑complete) – statement
- Examples of NP‑complete problems: 3‑SAT, Clique, Vertex Cover, Subset Sum

---

## Summary

This syllabus covers the entire official scope of Theory of Computation required for:

- University examinations (GATE, semester exams, GRE CS)
- Core computer science interviews (automata, language classification, decidability)
- Research foundation in computability and complexity

It includes all essential topics: finite automata, regular languages, pumping lemmas, context‑free grammars, pushdown automata, Turing machines, decidability, Rice’s theorem, Chomsky hierarchy, and an introduction to computational complexity (P, NP, NP‑completeness).

---

## ⭐ Support

If this syllabus helps you structure your learning or your GitHub repository, please **star** it to show your support.  
Contributions and corrections are welcome.
