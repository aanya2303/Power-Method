# CX/MATH 4640 Final Project
# Power-Method
```
---
Name: Aanya Khandelwal
Topic: 13 Power Method
Title: The Power Method: A comprehensive overview
----
```
## What is Power Method
Power Iteration or Power Method is an eigenvalue problem, that, when given a diagonalizabale matrix $A$, outputs the dominant eigenvalue of $A$. [source wiki here]

Given eigenvalues $\lambda_1, \lambda_2, \lambda_3, \ldots \lambda_n$ of an $n\times n$ matrix $A$, $\lambda_1$ is said to be the dominant eigenvalue if it satisfies the following conditions:
$$|\lambda_1| > |\lambda_i| $$ for all $i = 1, 2, 3, \ldots n$ [source here]

In order to perform power iteration on a matrix, the following conditions must be satisfied:
1. Matrix must be diagonalizable
2. Matrix must posses a single dominant eigenvalue
3. There must be a randomly chosen non-zero initial vector whose entries $\in R$

Power method is an iterative process that works on the following recurrence relation (given the aforementioned conditions): 
$$x_k = A\times x_{k-1} $$ 

[source here]
