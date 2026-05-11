---

---
- **elementwise multiplication** (Hadamard product)
$A \odot B = B\odot A$
$\begin{bmatrix}2 & 3 & 1\\0 & 8 & -2\end{bmatrix}\odot\begin{bmatrix}3 & 1 & 4\\7 & 9 & 5\end{bmatrix}=\begin{bmatrix}2\times 3 & 3\times 1 & 1\times 4\\0\times 7 & 8\times 9 & -2\times 5\end{bmatrix}=\begin{bmatrix}6 & 3 & 4\\0 & 72 & -10\end{bmatrix}$

- **matrix multiplication**
Review this!!!: for 1D array and column vectors is just the dot product
$\mathbf a \cdot \mathbf b=\mathbf a^\intercal \mathbf b$
$\begin{bmatrix}2 & -1 & 3 \end{bmatrix}\begin{bmatrix}4 \\ 6 \\ -2 \end{bmatrix}= 2\cdot4 + (-1)\cdot6 + 3\cdot(-2) = -6$
note $\mathbf a^\intercal \mathbf b=\mathbf b^\intercal \mathbf a \neq \mathbf a \mathbf b^\intercal$
$\mathbf a \mathbf b^\intercal$ is the **outer product** and has shape (n,n)


In PyTorch/NumPy:
- `*`→ **elementwise multiplication** (Hadamard product).
- `@`→ **matrix multiplication / dot product** (sums over features).

## In a linear model
$y = X w + b$
where:
- $X$ has shape $(n, d)$ = data matrix (n samples, d features),
- $w$ has shape $(d,)$ = weight vector,
- $b$ is a scalar bias,
- result $y$ has shape $(n,)$.


$$
X=
\begin{bmatrix}
1 & 2\\
3 & 4\\
5 & 6\\
7 & 8\\
9 & 10
\end{bmatrix},
\quad
w=
\begin{bmatrix}
10\\
100
\end{bmatrix},
\quad
b=0.5
$$

Dot product for first row:
$y_1 = 1\cdot 10 + 2\cdot 100 + 0.5 = 210.5$

## Difference between dot product and elementwise multiplication
```python
import torch

# 5 samples × 2 features
X = torch.tensor([[ 1.0,  2.0],
                  [ 3.0,  4.0],
                  [ 5.0,  6.0],
                  [ 7.0,  8.0],
                  [ 9.0, 10.0]])   # shape (5, 2)

w = torch.tensor([10.0, 100.0])    # shape (2,)
b = torch.tensor(0.5)              # scalar bias

# Correct: matrix multiplication
y_at = X @ w + b      # shape (5,)

# Wrong: just elementwise
y_mul = X * w + b     # shape (5, 2) ❌ not a dot product

# Manual fix: sum over features
y_sum = (X * w).sum(dim=1) + b   # shape (5,) ✅ same as @

print("y_at :", y_at)
print("y_mul:", y_mul)
print("y_sum:", y_sum)
```
