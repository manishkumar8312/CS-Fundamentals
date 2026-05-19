# COMPILER DESIGN

## Chapter 1: Introduction to Compilers

* What is a compiler? (Difference from interpreter and assembler)
* Need for compilers: source code to target machine code translation
* Major phases of a compiler (lexical → syntax → semantic → IR → code gen → optimizer)
* Passes: single-pass vs multi-pass compilers
* Front-end vs back-end
* Compiler construction tools (Lex, Yacc, etc.)

---

## Chapter 2: Lexical Analysis

* Role of lexical analyzer (scanner)
* Input buffering: one-buffer, two-buffer schemes, sentinels
* Tokens, patterns, lexemes
* Specifications of tokens using regular expressions
* Finite automata:
  * Deterministic Finite Automata (DFA)
  * Non‑deterministic Finite Automata (NFA)
  * Conversion: NFA → DFA (subset construction)
  * DFA minimization (Hopcroft’s algorithm – conceptual)
* From regular expressions to DFA (direct and via NFA)
* Lexical errors and error recovery (panic mode)

---

## Chapter 3: Syntax Analysis (Parsing)

### Context‑Free Grammars (CFG)

* Terminals, non‑terminals, start symbol, productions
* Derivations: leftmost, rightmost
* Parse trees and abstract syntax trees (AST)
* Ambiguity in grammars – causes and removal
* Eliminating left recursion
* Left factoring

### Top‑Down Parsing

* Recursive descent parsing (with backtracking)
* Predictive parsing (without backtracking)
* FIRST and FOLLOW sets – construction and significance
* LL(1) grammars: conditions, parsing table construction
* LL(1) parsing algorithm (stack‑based)
* Error recovery in LL(1)

### Bottom‑Up Parsing

* Handle pruning, handles, viable prefixes
* LR parsing overview: items, closure, goto
* LR(0) items and LR(0) automaton
* SLR(1) parsing – simple LR (most asked in GATE)
* Canonical LR(1) items
* LALR(1) parsing (lookahead LR)
* Shift‑reduce conflicts, reduce‑reduce conflicts
* Comparison: LL(1) vs SLR(1) vs LALR(1) vs LR(1)

### Error Handling in Parsing

* Panic mode recovery
* Phrase‑level recovery
* Error productions

---

## Chapter 4: Syntax‑Directed Translation (SDT)

* Syntax‑directed definitions (SDD)
* Inherited vs synthesized attributes
* Dependency graphs and evaluation order (topological sort)
* S‑attributed definitions (only synthesized)
* L‑attributed definitions (left‑to‑right, inherited allowed)
* Syntax‑directed translation schemes
* Building AST using SDT
* Translation of expressions, control flow statements, and declarations
* Type checking:
  * Type systems (static vs dynamic)
  * Type equivalence (name vs structural)
  * Type conversion (coercion)
  * Semantic errors

---

## Chapter 5: Intermediate Code Generation

* Need for intermediate representation (IR)
* Three‑address code (TAC):
  * Quadruples, triples, indirect triples
* Common TAC instructions: assignment, arithmetic, conditional/unconditional jumps, procedure calls
* Translation of expressions: syntax tree → TAC (using temporary variables)
* Translation of control flow:
  * If‑then‑else, while, do‑while, for loops
  * Short‑circuit code for logical operators (&&, ||)
* Translation of arrays: address calculation (row‑major, column‑major)
* Translation of procedures and function calls
* Handling of boolean expressions (backpatching – conceptual for GATE)

---

## Chapter 6: Symbol Table and Runtime Environment

### Symbol Table

* Information stored: name, type, scope, memory location, etc.
* Data structures for symbol tables (hash tables, linked lists, trees)
* Scopes: lexical (static) vs dynamic scoping
* Nested scopes and symbol table organization

### Runtime Environment

* Memory layout of a running program:
  * Code (text) segment
  * Data segment (initialized, uninitialized – BSS)
  * Stack segment
  * Heap segment
* Activation records (stack frames):
  * Structure: return address, local variables, parameters, previous frame pointer, static link (access link)
* Calling conventions: caller‑saved vs callee‑saved registers
* Heap management: malloc/free, garbage collection basics (mark‑and‑sweep, reference counting)
* Dangling pointers, memory leaks (conceptual)

---

## Chapter 7: Code Optimization

### Basic Concepts

* Basic blocks and flow graphs
* Leaders and partitioning into basic blocks
* Control flow graph (CFG)

### Machine‑Independent Optimizations

* Local optimizations (within a basic block):
  * Constant folding
  * Constant propagation
  * Copy propagation
  * Dead code elimination
  * Algebraic simplification
* Peephole optimization (window‑based)
* Global optimizations (across blocks):
  * Common subexpression elimination
  * Code motion (loop‑invariant code)
  * Induction variable elimination
  * Strength reduction (e.g., `x*2` → `x<<1`)
  * Loop unrolling, loop fusion/fission
  * Function inlining (conceptual)

### Data Flow Analysis

* Reaching definitions
* Live variable analysis
* Available expressions
* Very busy expressions
* Use‑define chains (ud‑chains) and def‑use chains (du‑chains)
* Data flow equation frameworks (forward/backward, may/must)

### Machine‑Dependent Optimizations

* Register allocation (graph coloring, spilling)
* Instruction scheduling (pipelining basics)

---

## Chapter 8: Code Generation

* Issues in code generation: instruction selection, register allocation, evaluation order
* Simple code generation from TAC (using stack or registers)
* Register allocation using graph coloring – basic idea
* Peephole optimization on target code
* Generating code for expressions (using Sethi‑Ullman algorithm – conceptual)
* Target machine models: stack machine vs register machine

---

## Chapter 9: Parsing Algorithms in Depth (Interview)


| Parser Type | Table Size | Power | Interview Importance |
|-------------|------------|-------|----------------------|
| Recursive Descent | None (code) | LL(1) with backtracking (or any unambiguous grammar) | High (coding) |
| LL(1) | Small | Deterministic top‑down | Medium |
| SLR(1) | Medium | LR(0) items + FOLLOW | Low |
| LALR(1) | Medium | Merged LR(1) states | Low |
| LR(1) | Large | Full LR(1) | Low |

* Converting ambiguous grammar to unambiguous for parsing
* Removing left recursion and left factoring – step‑by‑step
* Constructing CLR(1) and LALR(1) tables (GATE only)


---

## Chapter 10: Important Comparisons and Concepts for Interviews

* Compiler vs Interpreter vs Assembler
* Static linking vs Dynamic linking
* Static scoping vs Dynamic scoping
* Inherited vs Synthesized attributes
* DFA vs NFA (lexical analysis context)
* Top‑down vs Bottom‑up parsing
* SLR vs LALR vs LR(1)
* Three‑address code vs Abstract Syntax Tree
* Heap vs Stack memory
* Constant folding vs Constant propagation
* Recursion vs Iteration (in compiler implementation)

---

## Chapter 11: Miscellaneous & Advanced Topics 

* Directed acyclic graphs (DAGs) for common subexpression detection
* Parse tree vs AST vs DAG
* Attribute grammar evaluation strategies (top‑down, bottom‑up)
* Parameter passing mechanisms (call by value, reference, name, result)
* Handling of object‑oriented features (vtable, dynamic dispatch – basic)
* Just‑in‑time (JIT) compilation (conceptual)

---

## Chapter 12: Numerical and Problem‑Solving Practice

### Numerical Problems

* Computing FIRST and FOLLOW for a given grammar
* Checking if a grammar is LL(1) and building LL(1) table
* Building LR(0) items and determining SLR(1) conflicts
* Finding number of temporary variables in TAC for an expression
* Computing activation record size (parameters + locals + return address)
* Identifying loop‑invariant code
* Deriving basic blocks and flow graphs
* Applying constant propagation and dead code elimination

### Interview‑Style Problems

* "Write a regular expression to match valid variable names in C."
* "Design a DFA that accepts strings with equal number of 0s and 1s."
* "Implement a function to check balanced parentheses using stack."
* "Write a predictive parser for a simple arithmetic grammar."
* "Given an AST, generate three‑address code."
* "Explain the memory layout of this C program: `int x; static int y; int *p = malloc(10);`"
* "What happens when you call a function? Walk me through the stack frame creation."
* "How would you eliminate common subexpressions from a basic block?"

---

## Support

If this syllabus helps you crack GATE or land your dream job, consider giving it a star⭐. Contributions, corrections, and additional topic requests are always welcome. Keep compiling your success!