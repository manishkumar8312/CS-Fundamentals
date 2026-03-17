# Simplification and Normal Forms of CFG

## 12. Introduction

In many cases, a **Context-Free Grammar (CFG)** may contain unnecessary productions or symbols that make the grammar complex and difficult to analyze.

Before using CFGs in parsing algorithms or theoretical proofs, it is often necessary to **simplify the grammar**.

Simplification helps in:

* Making the grammar **easier to understand**
* Removing **redundant rules**
* Preparing the grammar for **normal forms**

Two widely used normal forms are:

* **Chomsky Normal Form (CNF)**
* **Greibach Normal Form (GNF)**

These normal forms are important in **compiler design**, **parsing algorithms**, and **formal language theory**.

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/4/4b/Context-free_grammar_parse_tree.svg" width="420"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/5/5a/Parse_tree_example.svg" width="420"/>
</p>

---

# 13. Simplification of Context-Free Grammars

Simplification involves removing productions that do not contribute to generating valid strings of the language.

The major steps include:

1. Removal of **null productions**
2. Removal of **unit productions**
3. Removal of **useless symbols**

These steps transform the grammar while preserving the **same language**.

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/2/2b/Formal_grammar_tree.svg" width="420"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/b/b8/CFG_derivation_tree.svg" width="420"/>
</p>

---

# 14. Removal of Null Productions

## 14.1 Definition

A **null production** is a production that derives the empty string.

```
A → ε
```

Here:

* **A** is a non-terminal
* **ε** represents the empty string

---

## 14.2 Why Remove Null Productions?

Null productions can complicate parsing and grammar analysis.
Therefore, they are usually removed before converting the grammar to **CNF or GNF**.

---

## 14.3 Steps to Remove Null Productions

1. Identify all **nullable variables**.
2. Create new productions by removing nullable variables.
3. Remove the **ε-production**.

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/0/07/Null_production_cfg_example.svg" width="420"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/6/6a/CFG_nullable_variable_example.svg" width="420"/>
</p>

---

## 14.4 Example

Original Grammar:

```
S → AB
A → aA | ε
B → b
```

Step 1: Nullable variable

```
A → ε
```

Step 2: Modify production

```
S → AB
S → B
```

Final Grammar

```
S → AB | B
A → aA | a
B → b
```

---

# 15. Removal of Unit Productions

## 15.1 Definition

A **unit production** is a production where a non-terminal derives another single non-terminal.

```
A → B
```

---

## 15.2 Why Remove Unit Productions?

Unit productions increase grammar complexity without adding new strings.

---

## 15.3 Steps to Remove Unit Productions

1. Identify all **unit productions**
2. Replace them with **direct productions**

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/e/e6/Unit_production_example_cfg.svg" width="420"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/9/94/Grammar_unit_production_removal.svg" width="420"/>
</p>

---

## 15.4 Example

Original Grammar

```
S → A
A → B
B → b
```

After removal

```
S → b
A → b
B → b
```

---

# 16. Removal of Useless Symbols

A symbol is useless if it does not help generate terminal strings.

Two types exist:

1. **Non-generating symbols**
2. **Unreachable symbols**

---

## 16.1 Non-Generating Symbols

Example

```
S → AB
A → a
B → C
C → D
```

If **D has no production**, then:

```
C, B
```

are useless.

---

## 16.2 Unreachable Symbols

Example

```
S → aA
A → b
B → c
```

Symbol **B** cannot be reached from **S**.

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/3/3b/CFG_reachable_symbols.svg" width="420"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/f/f7/Formal_grammar_graph.svg" width="420"/>
</p>

---

# 17. Normal Forms of CFG

Normal forms are standardized grammar structures used in parsing and theoretical proofs.

Two main normal forms:

1. **Chomsky Normal Form**
2. **Greibach Normal Form**

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/8/8c/Chomsky_normal_form_parse_tree.svg" width="420"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/4/4a/Greibach_normal_form_example.svg" width="420"/>
</p>

---

# 18. Chomsky Normal Form (CNF)

## 18.1 Definition

A grammar is in CNF if productions are:

```
A → BC
A → a
```

Exception

```
S → ε
```

---

## 18.2 Properties

1. Two non-terminals OR one terminal
2. No null productions
3. No unit productions
4. No useless symbols

---

## 18.3 Example CNF Grammar

```
S → AB
A → a
B → b
```

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/1/1c/CNF_parse_tree_example.svg" width="420"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/7/76/Formal_grammar_parse_tree.svg" width="420"/>
</p>

---

# 19. Conversion of CFG to CNF

Steps

### Step 1

Remove **null productions**

### Step 2

Remove **unit productions**

### Step 3

Remove **useless symbols**

### Step 4

Replace terminals in long productions

```
A → aB
```

Convert

```
X → a
A → XB
```

### Step 5

Break long productions

```
A → BCD
```

Convert

```
A → BX
X → CD
```

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/2/27/Grammar_transformation_example.svg" width="420"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/5/57/Chomsky_normal_form_transformation.svg" width="420"/>
</p>

---

# 20. Greibach Normal Form (GNF)

## 20.1 Definition

GNF productions have the form

```
A → aα
```

Example

```
S → aA
A → bB
B → c
```

---

## 20.2 Properties

1. Productions start with terminal
2. No left recursion
3. Used in **top-down parsing**

---

## 20.3 Example GNF Grammar

```
S → aA | bB
A → a
B → b
```

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/4/4a/Greibach_normal_form_example.svg" width="420"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/0/09/CFG_derivation_example.svg" width="420"/>
</p>

---

# 21. Conversion of CFG to GNF

Steps

1. Remove **null productions**
2. Remove **unit productions**
3. Remove **useless symbols**
4. Remove **left recursion**
5. Ensure productions start with **terminals**

Example

Original

```
S → AS | b
A → a
```

Converted

```
S → aS | b
A → a
```

---

# 22. Key Differences Between CNF and GNF

| Feature           | CNF              | GNF                 |
| ----------------- | ---------------- | ------------------- |
| Production form   | A → BC or A → a  | A → aα              |
| Used in           | CYK parsing      | Top-down parsing    |
| Terminals         | May appear alone | Always appear first |
| Parsing direction | Bottom-up        | Top-down            |

---

# 23. Summary

| Concept         | Description                          |
| --------------- | ------------------------------------ |
| Null Production | Production deriving ε                |
| Unit Production | Production A → B                     |
| Useless Symbols | Symbols that do not generate strings |
| CNF             | A → BC or A → a                      |
| GNF             | A → aα                               |

Simplifying grammars and converting them into **normal forms** helps in **efficient parsing, algorithm design, and theoretical analysis of languages**.

