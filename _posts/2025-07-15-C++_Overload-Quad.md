---
layout: post
title: "C++ Overload Review"
date: 2025-07-15 23:55:00 -0400
categories: [Class note review]
tags: [Class, Review]
---
# **Quad(Matrix) overload operator and Member Function**
```cpp
class Quad{
    // member variable
    array<double,4> m;
    static constexpr double tolerance = 10^-10;
    //Constructor
    quad::Quad(double a1,double a2,double a3,double a4){m{a1,a2,a3,a4};}
}
```
---
## **Special Quad Objects**
### zero matrix
```cpp
Quad Quad::zero(){
    return Quad(0,0,0,0); // return type Quad
}
```
---
### Identity Matrix
```cpp
Quad Quad::Identity(){
    return Quad(1,0,0,1);
}
```
---
## **Unary Operators**
### Addition
- overload to copy of the Matrix A
```cpp
Quad :: Quad operator+()const{
    return *this;
}
```
---
### Subtraction
- overload to copy of -A
```cpp
Quad:: Quad operator-()const{
    return m{-a1,-a2,-a3,-a4};
}
```
---
### prefix Increment ++A
- return Increment value of every element in Matrix A
```cpp
Quad& Quad operator++(){
    for(double&i:m){
        ++i;
    }
    return *this; // return the value of "this"
} // return type is reference because it will return the mdofiy the intial value 
```
---

### postfix increment A++
- Increment every element but return the old value
- ``*this`` will return the object iteself at this memory address in this case, it's returning ``Quad&``.
```cpp
Quad::Quad operator++(int){
    Quad temp = *this;
    ++(*this);
    return temp;
}
```
---
## **Binary Arithmetic Operators**
### Addition
- (A+B) => (a1+b1,a2+b2,a3+b3,a4+b4) => **Friend Function**
- Friend can make non-member function access to its private data;
```cpp
friend Quad operator+(const Quad& a, const Quad& b){
    return Quad(a.m[0]+b.m[0], a.m[1]+b.m[1],a.m[2]+b.m[2],a.m[3]+b.m[3]);
}
```
---
### Multiplication
- **Friend Function**, A ∗ B (a1b1 + a2b3, a1b2 + a2b4, a3b1 + a4b3, a3b2 + a4b4).
```cpp
friend Quad operator*(const Quad& a, const Quad& b){
    return Quad(a.m[0]*b.m[0],a.m[1]*b.m[1],a.m[2]*b.m[2],a.m[3]*b.m[3]);
}
```
---
### Division
- **Friend Function** A/B, A*B^-1.
```cpp
friend Quad operator/(const Quad& a, const Quad& b){
    if (b.zero()){return 0;}
    else{
        a*b.inverse();
    }
}
```
--- 

## **Quad specific Functions**

### **Determinant**
```cpp
double Quad determinant()const{
    return m[a0]*m[a3] - m[a1]*m[a2]; 
}//return a value which is double and the const here means the deter function is not allowed to modify the data.
```
---
### **Inverse**
```cpp
Quad::Quad inverse()const{
   double det = determinant(); // u cant use m.determinant(); because m is an array doesnt have dete class Quad has det method
   if(fabs(det)< EPSLION){
    throw runtime_error("cannot invert")
   }
   return Quad(m[3] / det,     // a4/det
        -m[1] / det,    // -a2/det
        -m[2] / det,    // -a3/det
        m[0] / det  );
}
```
---
### **Transpose**
```cpp
Quad::Quad Transpose()const{
    return Quad(m[0],m[2],m[1],m[3]);
}
```
---
### **Trace**
```cpp
double Quad::Trace()const{
    return m[0]+m[3];
}
```
---
### **Norm**
```cpp
double Quad::norm()const{
    return sqrt(m[0]*m[0] + m[1]*m[1] + m[2]*m[2] + m[3]*m[3]);
}
```
---
### **Condition Number**
```cpp
double Quad::condition_number()const{
    if(fabs(determinant())<tolerance){
        throw:: time_error("Matrix can be inverted")
    }
    else{
        double N = norm();
        Quad inv = inverse();
        return N* inv.norm();
    }
}
```
---
### **Is symmetric**
```cpp
bool Quad::is_symmetric()const{
    if (m == m.transpose())
}
```
---
