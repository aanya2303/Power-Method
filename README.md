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

## Proof of Power Method's convergence
It is known that the eigenvectors of a matrix form a basis using values $c_1, c_2, c_3, \ldots c_n$ that satisfy:
$$x = \sum_{i = 1}^k c_i v_i $$
This follows
$$x_0 = c_1 v_1 + c_2 v_2 + \ldots + c_n v_n$$
After one iteration of the basic power method (multiplication with $A$):
$$x_1 = A x_0 = c_1 v_1 \lambda_1 + c_2 v_2 \lambda_2 + \ldots + c_n v_n \lambda_n$$
$$\implies x_2 = A^2 x_0 = c_1 v_1 \lambda_1^2 + c_2 v_2 \lambda_2^2 + \ldots + c_n v_n \lambda_n^2$$
$$\implies x_k = A^k x_0 = c_1 v_1 \lambda_1^k + c_2 v_2 \lambda_2^k + \ldots + c_n v_n \lambda_n^k$$
$$\implies x_k = \lambda_1^k \bigg[c_1 v_1 + c_2 v_2 \bigg( \frac{\lambda_2}{\lambda_1}\bigg)^k + \ldots + c_n v_n \bigg( \frac{\lambda_n}{\lambda_1}\bigg)^k \bigg]$$
Given the initial assumption that $A$ must have a dominating eigenvector we know that $c_1 \neq 0$ and hence, the term $c_1 v_1$ dominates this equations when $k$ is very large.
According to the definition of dominating eigenvalue, we also know that $|\lambda_1|$ must be greater than $|\lambda_2|$ and so, $\big(\frac{\lambda_2}{\lambda_1}\big)^k$ becomes very small as $k$ becomes very large.

$$x_k \rightarrow c_1 v_1 \lambda_1^k \text{$\quad$as$\quad$    } k \rightarrow \infty$$

Therefore, the power method converges to calculates the dominating eigenvalue. 

Some observations:
1. The rate of convergence is linear
2. The rate depends on $\big |\frac{\lambda_2}{\lambda_1} \big|$

## Pseudocode
### Basic Power Iteration
```
def basic_PI(A):
  n, _ = shape(A)
  x_prev = random((n, 1))
  for i in range(threshold_value):
    x = A @ x_prev
    eig = x / x_prev
    x_prev = x
  return eig
```

### Normalized Power Iteration
The basic power method seen above involves many multiplications. With very small or very large values in the matrix $A$, it could quickly descend into an overflow or an underflow. To prevent this, a modified version of the power method normalizes the vector at each iteration. The value that converges to the eigenvalue is the norm. This is called Normalized Power Iteration.

```
def normalized_PI(A):
  n, _ = shape(A)
  x_prev = random((n, 1))
  for i in range(threshold_value):
    x = A @ x_prev
    norm_x = norm(x)
    x_prev = x / norm_x
  return norm
```
### Inverse Power Iteration
In the case that one requires the smallest magnitude eigenvalue instead of the largest, the fact that 
$$eigenvalue(A^{-1}) = 1 / eigenvalue(A) $$
Hence, in order to obtain the smallest magnitude eigenvalue, we perform inverse power iteration, which is power iteration with the inversed input matrix.

```
def inverse_PI(A):
  n, _ = shape(A)
  x_prev = random((n, 1))
  A_inv = inverse(A)
  for i in range(threshold_value):
    x = A_inv @ x_prev
    norm_x = norm(x)
    x_prev = x / norm_x
  return 1 / norm
```
**Note:** Instead of calculating the inverse (which is an expensive operation), one can find $x$ by solving the linear system $Ax = b$ using any more efficient method of choice.

### Shifted Power Iteration
