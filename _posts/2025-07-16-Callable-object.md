---
layout: post
title: "C++ Callable objects plus lambda expressions"
date: 2025-07-16 23:59:00 -0400
categories: [Class note review]
tags: [Class, Review]
---

# **Callable objects** 

## Function objects

Understand what means Fucntion Objects
---
**Ex: Standard Function Objects**.
```C++
Struct triple{
    int operator(int x){return 3*x}
}
int main(){
    tripe t
    cout << t(6)<< endl;
}
```
---
- when we create an object of triple t, Since it is **Callable Function objects** when use it,  we can simply say t(6).

