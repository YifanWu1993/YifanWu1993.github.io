---
layout: post
title: "C++ inheritance-vitual-Polymophism"
date: 2025-07-120 23:55:00 -0400
categories: [Class note review]
tags: [Class, Review]
---
# Inheritance
- **Synatx: `class derived_class_name : acess_specifier base_class_name`**
- *When acess_specifier is omitted, it will default to


---
## Construct Matrix by vector
- **Create 5x5 Matrix by filling with '*'**
```cpp
std::vector<vector<char>> marix(5,vector<char>(5, '*'));
```
---
- **resize** is a member function inside of **vector** function. syantx `resize(new_size, value)`.