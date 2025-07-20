---
layout: post
title: "Operating system Syc"
date: 2025-07-15 23:55:00 -0400
categories: [Class note review]
tags: [Class, Review]
---

# **Synchronization Tools**

## **Peterson's Solution**
- **Requirement:** 2 processes need to share two data items: `int turn;` and `boolean flag[2]`.
- **Turn** tells whose turn to enter the critical section.
- **Flag** array tells if a process is read to enter is CS.
## **Example Code**
- Assume we have Pi and Pj:
```cpp
While(True){
    flag[i] = true; // saying Pi is read to enter the CS
    turn = j; // saying it's j's turn to enter in the process.
    while(flag[j] && turn ==j); // means if j is occupy CS

    /* critical section*/  //if j is not occupy CS anymore, i can go in

    flag[i] = false; // when i finish occupying the CS, tell the OS it is not ready to enter by setting the flag[i] = false

    /*remainder section*/
}
```
- Brief explaniation of `while(flag[j] && turn ==j)`, if `flag[j] == True`, then it is bascially saying both Pi and Pj are ready to enter the CS, and Since here the second condition is `turn == j`, then it is j's turn, so j will enter in the CS, in other word the **While** loop will hang in there.

- **Bounded waiting:** The Core point here is two code for i and j will give the turn to their oppsite one then the while loop is to make sure if one finished CS the other one can enter right away. this prevent one process or threads keep occuping the CS forever.

- **Issues:** This does not prevent *“reorder the instruction"* which means OS might run the code in different order which might agaist the intention of code

---
# **Hardware Support for Synchronization**

## Mmeory Barriers
- Bascially this is a computer architectures instruction that force any changes in memory
## **Example:**
```cpp
while(!flag)
memory_barrier();
print x;
```
---
- This guarantee the **value of flag** is loaded before value of x.

## Test and Set
- Swap the contents of two words **atomically** to make it as an uninterruptible unit.
- when **Lock == True.** it means that the *lock* is locked so other process or threads couldn't get in the CS
- when **lock == False.** it means the lock is not locked anymore. so it allowed other thread or process to get in.
---
## **Code**
```cpp
boolean test_and_set(boolean *target){
    boolean rv = *target; // temporary rv to hold the paremter pass in 
    *target = true; // set the parameter to be true
    return rv; // Return the temp value that were holded for the pass in value.
}
```
---
- **Use case**
```cpp
lock = False; // Set the lock to be free.
while(True){
    while(test_and_set(&lock)); // lock is initalized set False so it will skip the while loop then set the lock to be **True**. So when other thread wanna come in it will lock them.
    
    operate(CS section); 

    lock = False;
}
```
---
- the **test_and_set** function will return the false for the current threads and set the lock to be true so others cannot get in.

## Compare_and_swap() // CAS
- Operates two words atomically by **swapping the content of two words**
- **understand of the concept:** the intialition of the value usually set to **expected** means the lock is free to enter in. The way it reset the pass in value is like what we did on test_and_set(), we made a temp value to hold the initial value we pass in then we switch to the new value to prevent other process or thread wanna come in.

---
## **Code**
```cpp
int compare_and_swap(int *value, int expected, int new_value){
    int temp = *value;
    if(*value == expected){*value = new_value}
    return temp;
}
```
---
- **Lock == expected means lock is Free to enter in**.
- **Lock == new_value means lock is occupied**.
---
## use case:
```cpp
lock = 0;
while(true){
    while(compare_and_swap(*lock, 0,1)!=0) // if it's equal to 0, it means the lock is free. it will jump to the CS section. // the function CAS here will return the value of 0 then set the lock to 1 to make sure no one can get in the lock/

    CS Section

    value = 0; // make sure after finished set the lock free again by assign the value to 0
}
```
---
- This one satisfies the **mutual - exclusion requirement**. but not **bounded - waiting requirement**.

- Understand again of **bounded - waiting requirement**. (say we have pi and pj 2 process. one must enter after another which means neither of them can keep occuping the CS forever.) *in other word*， neither of the process will be starved.
---
## Compare and swap fullfill bounded waiting requirement example:

## **Code**:





