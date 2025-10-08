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

#### **Argument Exchange**
---
- **The goal is to prove the greedy method wont lose the optimallicty. 

- Assume we have an **hypothetical optimal schedule $e'_1,e'_2 ... e'_k:$ with k activity which is the most optimal one**

- assume $e_1 \neq e'_1$, then **Since $e_1$ is the earliest termination.** so when we replace  $e_1$ with  $e'_1$,  $e'_2$ wont overlap with $e_1$. 
- **Therefore**, we can follow this logic and successfuly switch $e'_1 ... e'_k$ to $e_1 ... e_k$ without changing the **activity number k**. So we proof even we have a *optimal schedule*, we can replace to **greedy method**, without lose optimalicity.

#### **Induction**
---
- **base case:** n = 1, k = 1 is the optimal select
---
- **inductive hypothesis**
- 


---

## **Scheduling problems**

---




## **01 Knapsack Problem**

### **Problem Definition**
- **Container with Weight Capacity:** W ∧ Set of n items: i₁, i₂, ..., iₙ, each with:
  - **Value:** Vᵢ
  - **Weight:** Wᵢ
- **Goal:** Find Subset of items where `Total W ≤ Cw` ∧ `Max(V)`
- **Solve method:** Dynamic Programming (*this one cannot solve by greedy method*)
- **Note:** DP is for solving **Optimization Problems**. Also said can solve problems in **Sequence of decisions**

---

### **Example Problem**
- **Given:**
  - m ≤ 8, n = 4
  - P = {1, 2, 5, 6} (Prices/Values)
  - W = {2, 3, 4, 5} (Weights)
- **Find:** Max(Σ Pᵢ·Xᵢ) ∧ Σ wᵢ ≤ M, where Xᵢ ∈ {0, 1}

---

### **Dynamic Programming Algorithm**

### **DP-01-Knapsack Algorithm**

```
DP-01-Knapsack(W[1...n], P[1...n], W) // W[1...n] = weight for each element
D[0...n, 0...W] = 0  // Create Matrix     // P[1...n] = Price for every element
// W is the capacity
For i = 0 → n do ⇒ D[i, 0] = 0  // Set up 1st Column
For j = 0 → (W-1) do ⇒ D[0, j] = 0  // Set up 1st Row
For i = 1 ... n do  // i ≥ 2
  For j = 1 ... (W) do  // j ≥ 2
  D[i,j] = D[i-1, j]  // P[i] not in
    if w[i] ≤ j:
    D[i,j] = Max(D[i-1, j], D[i-1, j - w[i]] + P[i])
Return D[n, W]
```
---

---

### **DP Table Visualization**

### **Table Structure**
- **Rows (i):** Items (0 to n)
- **Columns (j):** Weight capacity (0 to W)
- **W → Column number**

| i \ W | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|-------|---|---|---|---|---|---|---|---|---|
| 0     | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| P₁ W₁ | 0 |   | 2 | 0 |   |   |   |   |   |
| 1 (2) | 0 |   | 0 |   |   |   |   |   |   |
| 2 (3) | 0 |   | 0 |   |   |   |   |   |   |
| 5 (4) | 0 |   | 0 |   |   |   |   |   |   |
| 6 (5) | 0 |   | 0 |   |   |   |   |   |   |

*i → Row number*

---

## **Decision Making**

### **Sequence of Decisions**
- **Making:** X₁, X₂, X₃, X₄


**Interpretation:** 
- Decision variables Xᵢ ∈ {0, 1} indicate whether to include item i
- The optimal solution involves selecting specific items based on the DP table

---

## **Key Concepts**
1. **Cannot solve by Greedy Method** - Requires Dynamic Programming
2. **Optimal Substructure** - Solution to larger problem depends on solutions to subproblems
3. **Memoization** - Store results in DP table to avoid recalculation
4. **Time Complexity:** O(n·W) - Pseudopolynomial time
5. **Space Complexity:** O(n·W) - For the DP table

---






