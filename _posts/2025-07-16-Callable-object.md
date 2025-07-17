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

