---
layout: post
title: "Operating system Syc"
date: 2025-07-15 23:55:00 -0400
categories: [Class note review]
tags: [Class, Review]
---

# **Synchronization Tools**
---
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
---
## Mmeory Barriers


