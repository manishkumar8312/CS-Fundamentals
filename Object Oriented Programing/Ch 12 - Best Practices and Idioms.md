# Chapter 12: Best Practices and Idioms

This chapter presents essential C++ best practices and idioms that lead to safer, more maintainable, and more efficient code. Mastering these patterns distinguishes novice C++ from professional C++.

## RAII – Every Resource Wrapped in an Object

RAII (Resource Acquisition Is Initialization) is the most important idiom in C++. It ties resource lifetime to object lifetime. Resources are acquired in constructors and released in destructors, ensuring automatic cleanup even when exceptions are thrown.

**Good practice – using RAII containers**:

```cpp
// Bad: manual resource management
void bad() {
    int* data = new int[1000];
    // ... if exception occurs here, memory leaks
    delete[] data;
}

// Good: RAII container
void good() {
    std::vector<int> data(1000);  // memory acquired in constructor
    // ... automatically released in destructor
}
```

**Custom RAII wrapper example**:

```cpp
class FileHandle {
    FILE* file;
public:
    FileHandle(const char* filename, const char* mode) {
        file = fopen(filename, mode);
        if (!file) throw std::runtime_error("cannot open file");
    }
    ~FileHandle() { if (file) fclose(file); }
    
    // Non-copyable, movable
    FileHandle(const FileHandle&) = delete;
    FileHandle& operator=(const FileHandle&) = delete;
    FileHandle(FileHandle&& other) noexcept : file(other.file) { other.file = nullptr; }
    FileHandle& operator=(FileHandle&& other) noexcept {
        if (this != &other) {
            if (file) fclose(file);
            file = other.file;
            other.file = nullptr;
        }
        return *this;
    }
    
    FILE* get() const { return file; }
};
```

## Copy‑and‑Swap for Strong Exception Guarantee

The copy‑and‑swap idiom provides strong exception safety for assignment operators. It also naturally supports both copy and move assignment with a single function.

```cpp
class String {
    char* data;
public:
    // ... constructors, destructor
    
    void swap(String& other) noexcept {
        std::swap(data, other.data);
    }
    
    // One assignment operator handles both copy and move
    String& operator=(String other) {  // pass by value
        swap(other);                   // non-throwing
        return *this;
    }
};
```

If a copy is needed, the parameter is copy‑constructed (may throw). If a move is possible, it is move‑constructed. The swap is no‑throw, so the original state is unchanged if any exception occurs before the swap.

## Pimpl Idiom (Pointer to Implementation)

The Pimpl idiom hides implementation details in a separate class, reducing compile‑time dependencies and improving build times. It also helps achieve binary compatibility.

**Header file (Widget.h)**:

```cpp
// Widget.h
#pragma once
#include <memory>

class Widget {
public:
    Widget();
    ~Widget();
    void doSomething();
    
private:
    struct Impl;
    std::unique_ptr<Impl> pImpl;
};
```

**Implementation file (Widget.cpp)**:

```cpp
// Widget.cpp
#include "Widget.h"
#include <iostream>

struct Widget::Impl {
    int internalData = 42;
    void helper() {
        std::cout << "Helper called\n";
    }
};

Widget::Widget() : pImpl(std::make_unique<Impl>()) {}
Widget::~Widget() = default; // requires definition here because Impl is incomplete in header

void Widget::doSomething() {
    pImpl->helper();
}
```

Benefits:
- Change implementation without recompiling client code.
- Hide compiler‑generated members.
- Minimise header inclusion.

## Non‑virtual Interface (NVI) Idiom

NVI suggests that public interfaces should be non‑virtual, and they call private or protected virtual functions. This enforces a template method pattern and adds pre‑/post‑condition checks in a central place.

```cpp
class Base {
public:
    // Public non-virtual interface
    void execute() {
        // pre-processing (e.g., logging, locking)
        doExecute();
        // post-processing
    }
    
private:
    virtual void doExecute() = 0;  // derived classes override this
};

class Derived : public Base {
private:
    void doExecute() override {
        // actual implementation
    }
};
```

Benefits:
- Control over invariants before and after the operation.
- Allows changes in the base class without affecting derived classes.

## Curiously Recurring Template Pattern (CRTP)

CRTP enables static polymorphism (compile‑time dispatch) without virtual function overhead. A derived class inherits from a base template with itself as the template argument.

```cpp
template <typename Derived>
class Shape {
public:
    void draw() const {
        static_cast<const Derived*>(this)->drawImpl();
    }
};

class Circle : public Shape<Circle> {
public:
    void drawImpl() const {
        std::cout << "Drawing a circle\n";
    }
};

class Square : public Shape<Square> {
public:
    void drawImpl() const {
        std::cout << "Drawing a square\n";
    }
};

template <typename T>
void render(const Shape<T>& shape) {
    shape.draw();  // compile-time dispatch
}
```

**Use cases**:
- Mixin classes (adding functionality).
- Counter for total number of instances of a class.
- Expression templates (Eigen, Boost.Proto).

## Rule of Zero

The Rule of Zero states that you should avoid writing custom destructors, copy/move constructors, and assignment operators. Instead, use RAII containers and smart pointers. The compiler‑generated special members behave correctly when all members are themselves RAII types.

```cpp
// Good – follows Rule of Zero
class Person {
    std::string name;
    std::vector<int> scores;
public:
    // No custom destructor, copy/move, or assignment needed
    Person(const std::string& n) : name(n) {}
    void addScore(int s) { scores.push_back(s); }
};
```

If you must manage a resource, encapsulate it in a separate RAII class. Then the owning class remains simple.

## Const Correctness

Use `const` everywhere it makes sense: on variables, parameters, member functions, and return types. This prevents accidental modifications and improves code readability.

```cpp
class DataProcessor {
    std::vector<int> data;
public:
    void add(int x) { data.push_back(x); }  // non-const member
    
    int getSum() const {  // const member – does not modify object
        int sum = 0;
        for (int v : data) sum += v;
        return sum;
    }
    
    const std::vector<int>& getData() const { return data; }  // const reference
};

void process(const DataProcessor& dp) {
    int sum = dp.getSum();  // OK
    // dp.add(5);  // Error: cannot call non-const on const reference
}
```

**Guidelines**:
- Declare member functions `const` if they do not modify the object’s logical state.
- Pass parameters by `const&` unless you need a copy or modification.
- Use `const` iterators (`cbegin()`, `cend()`) when not modifying.

## Prefer `nullptr` over `NULL` or `0`

`nullptr` is a pointer literal of type `std::nullptr_t` that converts to any pointer type but not to integers. It eliminates ambiguity and overload resolution problems.

```cpp
void f(int) { std::cout << "int\n"; }
void f(char*) { std::cout << "char*\n"; }

int main() {
    f(0);       // calls f(int)
    f(NULL);    // may call f(int) if NULL is 0
    f(nullptr); // calls f(char*) – correct
}
```

## Use `enum class` Instead of Plain `enum`

Scoped enumerations (C++11) provide type safety, explicit scope, and better forward declaration.

| Property | `enum` (unscoped) | `enum class` (scoped) |
|----------|-------------------|----------------------|
| Implicit conversion to int | Yes | No |
| Scoping | Enumerators leak into enclosing scope | Enumerators require `EnumName::` |
| Underlying type | Implementation‑defined (unless specified) | Default `int`, can be specified |
| Forward declaration | Only if underlying type specified | Yes (by default) |

```cpp
// Bad: unscoped enum
enum Color { Red, Green, Blue };
int c = Red;  // implicit conversion – dangerous

// Good: scoped enum
enum class Color { Red, Green, Blue };
Color c = Color::Red;
// int i = Color::Red;  // Error: no implicit conversion
```

## Avoid Raw `new`/`delete` – Use Smart Pointers and Containers

Modern C++ should rarely use explicit `new` and `delete`. Prefer:

- **Automatic storage** (stack allocation) – fastest and safest.
- **Containers** (`std::vector`, `std::string`) for arrays.
- **Smart pointers** (`std::unique_ptr`, `std::shared_ptr`) for dynamic objects.

```cpp
// Bad
int* p = new int(42);
delete p;

// Good
auto p = std::make_unique<int>(42);  // unique_ptr manages memory

// Bad
int* arr = new int[100];
delete[] arr;

// Good
std::vector<int> arr(100);
```

## `override` and `final` Specifiers

- `override` – declares that a virtual function overrides a base class function. The compiler checks signature compatibility, catching mistakes early.
- `final` – prevents further overriding of a virtual function or prevents a class from being inherited.

```cpp
class Base {
public:
    virtual void foo(int);
    virtual void bar() final;
    virtual ~Base() = default;
};

class Derived : public Base {
public:
    void foo(int) override;   // OK
    // void foo(double) override; // Error: no matching base function
    // void bar() override;   // Error: bar is final in Base
};

class FinalClass final : public Base {
    // This class cannot be inherited further
};
```

Using `override` is essential for maintainable polymorphic hierarchies. It transforms silent errors into compile‑time errors.

## Summary Table – Best Practices Cheat Sheet

| Practice | Key Benefit | Code Example |
|----------|-------------|---------------|
| RAII | Automatic resource cleanup | `std::vector<int> v(100);` |
| Copy‑and‑swap | Strong exception safety | `String& operator=(String other) { swap(other); return *this; }` |
| Pimpl | Reduce compile‑time dependencies | `std::unique_ptr<Impl> pImpl;` |
| NVI | Control pre/post behaviour | Public non‑virtual calling private virtual |
| CRTP | Static polymorphism | `class Derived : public Base<Derived>` |
| Rule of Zero | Simplicity, fewer bugs | Use RAII members only |
| Const correctness | Prevent unintended modification | `int get() const { return x; }` |
| `nullptr` | Type‑safe null pointer | `int* p = nullptr;` |
| `enum class` | Scoped, no implicit conversions | `enum class Color { Red };` |
| Smart pointers | Ownership management | `auto p = std::make_unique<T>();` |
| `override` | Catch signature errors | `void foo() override;` |
| `final` | Prevent further overriding/inheritance | `class C final { };` |

Adopting these best practices will significantly improve the quality, safety, and readability of your C++ code. They are not merely stylistic preferences – they are essential tools for writing professional C++.