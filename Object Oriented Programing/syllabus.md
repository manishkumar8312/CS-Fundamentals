# OBJECT ORIENTED PROGRAMMING IN C++

## Chapter 1: Introduction to OOP and C++ Basics

* Procedural vs Object-Oriented Programming
* Benefits of OOP: modularity, reusability, maintainability
* Core OOP concepts:
  * Encapsulation
  * Abstraction
  * Inheritance
  * Polymorphism
* C++ as a multi‑paradigm language (procedural, OOP, generic, functional)
* Basic C++ syntax review:
  * Input/output (cin, cout, cerr)
  * Namespaces (std, custom)
  * References vs pointers
  * Dynamic memory: new, delete, new[], delete[]
  * Function overloading and default arguments

---

## Chapter 2: Classes and Objects

* Defining a class: access specifiers (public, private, protected)
* Data members and member functions
* Creating objects: stack vs heap allocation
* Accessing members: dot (.) and arrow (->) operators
* **`this` pointer** – implicit reference to current object
* Static members:
  * Static data members (shared across all objects)
  * Static member functions (can only access static members)

### Constructors and Destructor

* Default constructor
* Parameterized constructor
* Constructor overloading
* Constructor with default arguments
* Copy constructor (shallow vs deep copy)
* **Member initializer list** – best practices for initialization
* Destructor: role and execution order
* `explicit` keyword to prevent implicit conversions

---

## Chapter 3: Encapsulation and Data Hiding

* Why encapsulation matters – protecting internal state
* Getters (accessors) and setters (mutators)
* Const correctness:
  * Const objects and const member functions
  * Const member variables (initialized via initializer list)
* Friend functions and friend classes:
  * When and why to use `friend`
  * Trade‑offs: breaking encapsulation vs convenience
* Mutable keyword – modifying a member inside a const object

---

## Chapter 4: Inheritance

* Base class and derived class syntax
* Access specifiers in inheritance: public, protected, private
  * Effect on member accessibility in derived classes
* **Types of inheritance**:
  * Single inheritance
  * Multiple inheritance
  * Multilevel inheritance
  * Hierarchical inheritance
  * Hybrid inheritance (diamond problem)

### Order of Constructor/Destructor Calls

* Construction: base → derived
* Destruction: derived → base
* Passing arguments to base class constructor

### Diamond Problem and Virtual Inheritance

* Virtual base classes
* How virtual inheritance resolves ambiguity
* Memory layout considerations

### `using` Declaration in Derived Classes

* Restoring access to base class members

---

## Chapter 5: Polymorphism

### Compile‑Time Polymorphism (Static)

* Function overloading
* Operator overloading (see Chapter 6)

### Run‑Time Polymorphism (Dynamic)

* **Virtual functions** – mechanism and vtable
* Overriding vs hiding
* `override` specifier (C++11)
* `final` specifier (prevents further overriding or inheritance)

### Abstract Classes and Interfaces

* Pure virtual functions (`= 0`)
* Abstract class – cannot instantiate
* Interface emulation in C++ (class with only pure virtual functions)

### Virtual Destructors

* Why base class destructor should be virtual
* Undefined behaviour if deleting derived object via base pointer without virtual destructor

### Run‑Time Type Information (RTTI)

* `typeid` operator and `type_info` class
* `dynamic_cast` (safe downcasting)
* When RTTI is necessary – and when to avoid it

---

## Chapter 6: Operator Overloading

* Rules and limitations of operator overloading
* Overloading as member function vs non‑member (friend) function

### Unary Operators

* `++` (prefix and postfix)
* `--`
* `!`, `~`, `-` (unary minus)

### Binary Operators

* Arithmetic: `+`, `-`, `*`, `/`, `%`
* Relational: `==`, `!=`, `<`, `>`, `<=`, `>=`
* Assignment: `=` (deep copy, copy‑and‑swap idiom)
* Compound assignment: `+=`, `-=`, etc.
* Subscript operator `[]` (const and non‑const versions)
* Function call operator `()` – functors
* Stream insertion `<<` and extraction `>>` (must be non‑member)

### Overloading `new` and `delete`

* Custom memory management for a class

---

## Chapter 7: Exception Handling

* Traditional error handling vs exceptions
* C++ exception keywords: `try`, `catch`, `throw`
* Throwing exceptions from constructors and destructors
* Catch by value, reference, or pointer – best practice (catch by const reference)
* Standard exception hierarchy (`<stdexcept>`):
  * `std::exception`, `std::logic_error`, `std::runtime_error`
  * `std::bad_alloc`, `std::bad_cast`, etc.
* Exception specifications (deprecated) vs `noexcept` specifier
* Stack unwinding and resource management
* RAII (Resource Acquisition Is Initialization) as the key to exception‑safe code

---

## Chapter 8: Templates (Generic Programming)

### Function Templates

* Syntax and type deduction
* Template instantiation
* Overloading function templates

### Class Templates

* Defining a generic class (e.g., `Stack<T>`)
* Member functions defined inside/outside the class template
* Template specialization (full and partial)
* Non‑type template parameters (e.g., `array<T, N>`)

### Variadic Templates (C++11)

* `sizeof...` operator
* Recursive expansion and fold expressions (C++17)

### Template Metaprogramming (basic concepts)

* Compile‑time computations
* `static_assert` for compile‑time checks

---

## Chapter 9: Standard Template Library (STL)

### Overview

* Containers, iterators, algorithms, functors, allocators
* Complexity guarantees

### Containers

| Category       | Examples                                      |
|----------------|-----------------------------------------------|
| Sequence       | `vector`, `deque`, `list`, `forward_list`, `array` |
| Associative    | `set`, `multiset`, `map`, `multimap`          |
| Unordered      | `unordered_set`, `unordered_map`, etc.        |
| Container adaptors | `stack`, `queue`, `priority_queue`        |

### Iterators

* Input, output, forward, bidirectional, random‑access
* Iterator invalidation rules (especially for `vector`)
* Reverse iterators (`rbegin`, `rend`)

### Common Algorithms (`<algorithm>`)

* Sorting, searching, partitioning, heap operations
* Min/max, permutations, numeric algorithms (`<numeric>`)

### Functors (Function Objects)

* Predefined functors (`std::plus`, `std::greater`, etc.)
* Lambda expressions (C++11) – syntax, capture lists, mutable lambdas
* `std::function` – type erasure for callables

### Smart Pointers (C++11)

* `std::unique_ptr` (exclusive ownership)
* `std::shared_ptr` (reference‑counted)
* `std::weak_ptr` (breaking cycles)
* `std::make_unique` / `std::make_shared`

---

## Chapter 10: Advanced C++ Features

### Move Semantics and Perfect Forwarding

* Lvalue and rvalue references (`&&`)
* Move constructor and move assignment operator
* Rule of Five (Rule of Three + move operations)
* `std::move` and `std::forward`
* Copy‑and‑swap idiom

### Type Traits and `type_traits` Header

* `is_integral`, `is_class`, `enable_if`, etc.
* SFINAE (Substitution Failure Is Not An Error) – basic concept
* `decltype` and `auto` type deduction

### User‑Defined Literals

* Creating custom literals (e.g., `"hello"_s` for `std::string`)

### Concurrency Basics (C++11 and later)

* `std::thread`, `std::jthread` (C++20)
* `std::mutex`, `std::lock_guard`, `std::unique_lock`
* `std::async` and `std::future` / `std::promise`
* Atomic types (`std::atomic`)

---

## Chapter 11: Design Patterns in C++ (Overview)

* Creational patterns:
  * Singleton (thread‑safe versions)
  * Factory Method, Abstract Factory
  * Builder
* Structural patterns:
  * Adapter (using inheritance and composition)
  * Decorator
  * Proxy
* Behavioural patterns:
  * Observer (using `std::function` callbacks)
  * Strategy
  * Command
  * State
* RAII as a pattern – resource management

---

## Chapter 12: Best Practices and Idioms

* **RAII** – every resource wrapped in an object
* **Copy‑and‑Swap** for strong exception guarantee
* **Pimpl Idiom** (Pointer to Implementation) – reducing compile‑time dependencies
* **Non‑virtual Interface (NVI)** idiom
* **Curiously Recurring Template Pattern (CRTP)** – static polymorphism
* **Rule of Zero** – let the compiler generate special members
* Use `const` wherever possible (const correctness)
* Prefer `nullptr` over `NULL` or `0`
* Use `enum class` instead of plain `enum`
* Avoid raw `new`/`delete` – use smart pointers and containers
* `override` and `final` specifiers

---

## Chapter 13: Debugging, Testing, and Tools

* Compilation process: preprocessing, compilation, assembly, linking
* Common compiler flags: `-Wall`, `-Wextra`, `-Werror`, `-std=c++17`
* Debugging with `gdb` or `lldb`
* Sanitizers: AddressSanitizer, UndefinedBehaviorSanitizer
* Unit testing frameworks: Google Test, Catch2
* Code formatting: `clang-format`
* Static analysis: `clang-tidy`, `cppcheck`
* Profiling: `gprof`, `perf`, `valgrind`

---

## Chapter 14: Hands‑on Projects and Problem Sets

### Beginner

* Bank account system (encapsulation, constructors)
* Polynomial class with operator overloading
* Generic dynamic array template (similar to `std::vector`)

### Intermediate

* `String` class implementation (deep copy, move semantics, reference counting optional)
* Shape hierarchy (abstract base class, polymorphic drawing)
* Expression evaluator (using stack, functors, or inheritance)
* Simple `shared_ptr` implementation (template, reference counting)

### Advanced

* Thread‑safe queue for producer‑consumer
* Small STL‑like container (with iterators, allocator support)
* Event system using observer pattern and `std::function`
* Memory pool / custom allocator

---

## Chapter 15: Comparison with Other OOP Languages

* C++ vs Java:
  * Multiple inheritance, operator overloading, pointers
  * Destructors vs garbage collection
  * Stack‑allocated objects (no `new` for every object)
* C++ vs C#:
  * Properties vs getter/setter
  * Value types and references
* C++ vs Python:
  * Static typing vs dynamic typing
  * Performance
* Where C++ shines: system programming, real‑time, game engines, embedded systems

---

## Support

If this syllabus helps you master Object Oriented Programming in C++, please ⭐ star the repository. Contributions, suggestions, and corrections are always welcome. Happy coding!