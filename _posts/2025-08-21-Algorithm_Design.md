---
layout: post
title: "Algorithm_Design"
date: 2025-08-21 23:55:00 -0400
categories: [Class note review]
tags: [Class, Review, Algorithm Design]
---

# **Algorithmic Recurrences**
---
- If the question is small enough, T(n) = theta(1). For ex, we have one element in ``Array[]``

# **Greedy Algorithm**
- Greedy Algorithm usually is to Fnid the optmize Solution such as Find the **Max** or **Min** Solution.
- **Step:** Find the Feasible solution then optimal that feasible solution 
---
## **Activity Selection prblem**
- **Definition:** Find the max number of the activity can happen without the overlap in the hall
![Activity Chart](Activity_selection.PNG "Activity Selection Example")

---
### **Normal Approach**
---
- **Step 1: Normal approach** with an unsorted activity list, lets find the eariest $f_i$(which refer to the eariest finish time of a actiity). **Then,** we set this  $f_i$ as our start value saying ``` k =  $f_i$``` 

- **Step 2:** Since **the goal** is to Find the Max number of Activity can appear on the hall without Overlapping and we have our first value k which is the earliest finish time of all the activity. **Therefore,** the way to do it is to find the next activity of $S_i$ >= k and compare all the **feasible $S_i$** to find the minimum among it and it is our second activity, then we keep this process until we finished

---

- **Normal approach Conclusion:** Finding the feasible solution and the minimum among them in unsorted Activity List.
- Worst case For finding all the feasable solution which is $(n-1) + (n-2) + .... 1  = n*(n-1)/2$.
- The comparison of min is operated it through the process of finding feasible solutions. Meaning every step of iteration we got **$2(n-1)$ instead of $(n-1)$**. But still it is a Linear cost.
- Therefore this algorithm without using greedy method is **$(n-1) + (n-2) + .... 1  = n*(n-1)/2$.** which is **$O(n^2)$**.

---

### **Greedy Approach**
---

- **Step1:** Sort the activity list base on $f_i$. For ex:
             $i=1: [1,3]$
             $i=3: [3,5]$
             $i=5: [3,6]$
             $i=7: [5,7]$
             $i=8: [7,8]$
             $i=2: [4,9]$
             $i=4: [6,10]$
             $i=6: [9,10]$
             $i=9: [4,11]$
    **Sorted cost is $O(nlogn)$**, then Once we have sorted it, we can write our algorithm below
    ```
    Greedy-Activity-select(s,f,n):
    //s,f are sorted finish and start
    // n is the number of activities
    k  = 1
    A = f_1;
    For i =2 to n do:
      if s_i >= A:
        k += 1
        A = f_i;
    ```
- **Above algorithm actually only tell u how many acitiviy u can max it out but not telling u the exact actitity number**

- The cost here is $O(n)$ Since its sorted already so the final cost is **$nlog(n) + n = O(nlog(n))$**. 

---

- **same greddy Algorithm But the result will show Selected activity
```
Greedy-Activity2(s,f,n)
// s and f is sorted
A = [a1]
k = 1
for i = 2 to n do
  if f_(i) <= s_k
    A.append(ai)
    k = i 
```
---

- **Here is the result**
![Activity Chart](Result.PNG "Activity Selection Example")


### **Proof by (exchange argument or Induction)**

