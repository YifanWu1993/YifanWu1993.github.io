---
layout: post
title: "C++ Callable objects plus lambda expressions"
date: 2025-07-16 23:55:00 -0400
categories: [Class note review]
tags: [Class, Review]
---


# **Callable objects** 

## Function objects

Understand what means Fucntion Objects
---
**Ex: Standard Function Objects**.
```cpp
struct triple {
    int operator()(int x) { return 3 * x; }
};

int main() {
    triple t;
    std::cout << t(6) << std::endl;
}
```
---
- when we create an object of triple t, Since it is **Callable Function objects** when use it,  we can simply say t(6).
---
## Callable Standard Library Operators

In C++, the STL provides standard function objects (also called functors) for common operations.  
- **Binary** means the operator takes **two inputs** (e.g., `a + b`).
- **Unary** means the operator takes **one input** (e.g., `-a`).

### Arithmetic Function Objects

| Type     | Functor Name         | Arity  |
|----------|----------------------|--------|
| plus     | `plus<T>`            | Binary |
| minus    | `minus<T>`           | Binary |
| multiplies | `multiplies<T>`    | Binary |
| divides  | `divides<T>`         | Binary |
| modulus  | `modulus<T>`         | Binary |
| negate   | `negate<T>`          | Unary  |

### Relational Function Objects

| Functor Name         | Description          |
|----------------------|---------------------|
| equal_to<T>          | `==`                |
| not_equal_to<T>      | `!=`                |
| greater<T>           | `>`                 |
| greater_equal<T>     | `>=`                |
| less<T>              | `<`                 |
| less_equal<T>        | `<=`                |

### Logical Function Objects

| Functor Name         | Description      | Arity  |
|----------------------|-----------------|--------|
| logical_and<T>       | logical AND     | Binary |
| logical_or<T>        | logical OR      | Binary |
| logical_not<T>       | logical NOT     | Unary  |

**Note:**  
- *Binary*: needs two arguments, like `plus<T>()(a, b)`.
- *Unary*: needs one argument, like `negate<T>()(a)`.

---

**Example:**  
```cpp
#include <functional>
#include <iostream>

int main() {
    std::plus<int> add;
    std::negate<int> neg;

    std::cout << add(3, 4) << std::endl;  // Output: 7
    std::cout << neg(5) << std::endl;     // Output: -5W
}
```
---
- **Callable object** = an object that u can "**Call**" with parentheses, just like **function:** `obj(args)`.
- after class has overloaded `operator()`, it is an **callable object**.
---

**Example 2:**
```cpp





