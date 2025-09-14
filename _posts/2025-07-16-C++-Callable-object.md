---
layout: post
title: "C++ Callable objects plus lambda expressions"
date: 2025-07-16 23:55:00 -0400
categories: [Class note review]
tags: [Class, Review, C++]
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
    std::cout << neg(5) << std::endl;     // Output: -5
}
```
---
- **Callable object** = an object that u can "**Call**" with parentheses, just like **function:** `obj(args)`.
- after class has overloaded `operator()`, it is an **callable object**.
---

**Example 2:**
- An ex Class with normal member function and overload Functors()
---
```cpp
class foo{
    private:
     int x;
    public:
    int &square(int &y){
        y = y*y;
        return y;
    } // member function
    int operator()(){
        return x+x+x;
    }
};

int main(){
    foo f;
    f.square(5); // use function member
    cout << f() << endl;
}
```

---
## **Lambda Expressions**

- **Syntax:** [Capture] (parameters) -> return_type {body}
---
### Usage (Callable object consider as first class citizen)
#### **Assigning lambda to variable**
- **Ex:**
```cpp
auto square = [](int n){return n*n;};
square(6);
 ```
 - so here we assign lambda to "square".

 ---
 #### **Return a lambda from a function**
- **Ex:**(bascially a function return lambda)
```cpp
auto make_multiplier(int factor){
    return [factor](int x){return x*factor;};
}

int main(){
    auto t = make_multiplier(10); // pass the factor as 10 here.
    t(5);// 5*10 = 50
    t(10);//10*10 = 100
}
```
---
#### **Pass lambda as a parameter to a function**
- **Ex:**
```cpp
// use lambda as parameter in our function
void addmore(int x, int y, auto func){
    cout << func(x,y) << endl;
}//the parameter "auto func" means u can pass any type of parameter even the lambda.
// main
int main(){
    // our lambda
    auto add =[](int a, int b){return a+b;};
    // call addmore by pass in parameter.
    addmore(3,7,add); // this will return 10
    // pass lambda directly
    addmore(5,3,[](int a, int b){return a*b;}); // print 15
}
```
- here we had a function "*addmore(auto func)*", one parameter is "auto func", which **auto** let u to pass lambda as a parameter

---

#### Mutable in Lambda
- **EX:**
```cpp
int main(){
    int count = 0;
    auto lambda =[=](){ return count ++;}; // this will give u error since in lambda, it was consider const under the hood
    // The way u can modify
    auto lambda =[=]() mutable{
        count ++;
        cout << count << endl;
    }// this will return count = 1

    // NOTICE: the count is modiy inside scope of the lambda the actual "Count" in the memory will still be 0
    cout << count << endl; // this will still return 0.
}
```
---
- **Another Ex of modify the value in lambda with reference**
---
```cpp
int main(){
    int b = 11;
    int a = 5;
    auto ss = [a,&b](){
        b += a;
        a += b;
    };
    ss(); 
    // even out of the scope b will be modify because b was passed by reference
    cout << b << endl; // b = 16.
    // but a will never changed since its pass by value
    cout << a << endl; // a = 5.
}
```
---
- **Ex of explicity define the return type**
---
```cpp
int main(){
    auto lambda = [](int a, int b) -> double{
        return static_cast<double>(a)/b;
    };
    // static_cast<double> transfer the parameter int a and b to double
    lambda(5,2);
}
```
---
## **Function Pointers:**
- **synatx:** `Returntype (*FunctionPtrName)(parameterTypes)`, `FunctionPtrName = FunctionName`, `FunctionPtrName(arguments)`.
---
- **Ex of assign function to function pointer.**
---
```cpp
double average(int x, int y){return (x+y)/2.0;}
int quotient(int x, int y){return x/y;}
int remainder(int x, int y){return x%y;}

int (*foo)(int,int);

int main(){
    foo = average; // error, since the return type of foo is int, average is double so complier will give error.
    foo = quotient; // success
    foo = remainder; // success
    cout << foo(12,9)<<endl;
}
```
---
- **Ex of Function taking Function pointer as Parameters.**
---
```cpp
double eval(int(*func)(int,int),int a ,int b){
    return func(a,b); // you can also use funtion pointer as a return type.
}
// So the most important thing is pass a function which has the same return type as a parameter
int main(){
    cout << eval(remainder,12,9) << endl; // return 3
    cout << eval(average,12,9)<< endl; // error since the return type one is double and one is int.
}
```
- **If u use function pointer as a parameter to a Function like the Ex above, u can pass an exist function as parameter and also you can return that function pointer also**
---

## **Function type**

- **Snytax:** `function<int(int,int)> func;`. **It means wrap functions taking two ints and return int**.
- `func` **can hold free functions, lambdas or fucntors that match** `int(int,int)`.
---
- **Ex**:
```cpp
// Free Function
int multiplity(int a, int b){return a*b;}

// Functor
struct adder{
    int operator()(int a, int b){return a+b;}
};

// Define Function type.
function<int(int,int)> func;

// Assign function "mulitplity" to func.
func = multiplity;
cout << func(2,3) << endl; // print 6

// Functor ->  Callable Object
func = adder();
cout << func(1,2) << endl; // print 3

// Lambda sign to a Function type
func = [=](int a,int b){return a+b;};
func(3,4);
```