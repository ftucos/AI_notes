---

---
In linear algebra, **factoring a matrix** means expressing it as a product of simpler matrices. This is done to reveal the geometric meaning of a linear transformation, or simplify computations

**Diagonalizing** a square matrix (i.e. a linear transformation) means rewriting it as a sequence of three steps:
1. **change of basis** (rotate / realign the coordinate system)
2. **scale independently along each axis**
3. **return to the original basis**

In other words, we try to find a coordinate system in which the transformation acts only as **axis-wise scaling (diagonal matrix)**.

---
## Eigendecomposition method
This is the easiest approach and works for square matrices $\boldsymbol{A}\in\mathbb{R}^{n\times n}$
**Eigenvectors** are vectors that:
- do **not change direction** under the transformation
- are only **scaled** by a factor (the eigenvalue)

If we can find $n$ **linearly independent eigenvectors**, then they form a **new basis** of the space.
In this basis, the transformation {the scaling matches the eigenvalues} becomes diagonal.
If the matrix is diagonalizable, it can be written as:
$\boldsymbol{A} = \boldsymbol{Q}\boldsymbol{\Lambda}\boldsymbol{Q}^{-1}$
where:
- $\boldsymbol{Q}$: matrix of eigenvectors (change of basis)
- $\boldsymbol{\Lambda}$: diagonal matrix of eigenvalues (scaling)
- $\boldsymbol{Q}^{-1}$: inverse change of basis

$$\boldsymbol{A}
=
\underbrace{\boldsymbol{Q}}_{\text{change basis}}\,
\underbrace{\boldsymbol{\Lambda}}_{\text{scale axes}}\,
\underbrace{\boldsymbol{Q}^{-1}}_{\text{restore basis}}$$
### When the matrix can be eigendecomposed
4. **All eigenvalues are distinct**
5. **Some eigenvalues are repeated **but the algebric multiplicity matches the geometric multiplicity

# Singular Value Decomposition (SVD)
The **Singular Value Decomposition** is a more general matrix factorization that extends eigendecomposition to:
- non-square matrices
- rank-deficient matrices
- matrices that are not diagonalizable

> [!note]+ **Note on non-square  and rank-deficien matrices**
> Rectangular matrices can be conceptualized as transformations that suppress or appends some dimensions. SVD handles that
> $$\boldsymbol{A}\boldsymbol{x} =
> \begin{bmatrix}
> 1 & 0 \\
> 0 & 1 \\
> 0 & 0
> \end{bmatrix}
> \begin{bmatrix}
> x_1 \\
> x_2
> \end{bmatrix}
> =
> \begin{bmatrix}
> x_1 \\
> x_2 \\
> 0
> \end{bmatrix}$$
> $$\boldsymbol{B}\boldsymbol{y} =
> \begin{bmatrix}
> 1 & 0 & 0 \\
> 0 & 1 & 0
> \end{bmatrix}
> \begin{bmatrix}
> y_1 \\
> y_2 \\
> y_3
> \end{bmatrix}
> =
> \begin{bmatrix}
> y_1 \\
> y_2
> \end{bmatrix}$$

The decomposition is:
$\boldsymbol{A} = \boldsymbol{U}\boldsymbol{\Sigma}\boldsymbol{V}^T$
where:
- $\boldsymbol{U}$: left singular vectors
- $\boldsymbol{V}$: right singular vectors
- $\boldsymbol{\Sigma}$: diagonal matrix of **singular values** $\sigma_i$

Key differences from eigendecomposition:
- left and right singular vectors are **different**
- singular vectors are **always orthogonal **(eigenvectors instead just need to be linearly independent)
- singular values are always **non-negative**

> [!note]+ **Details**
> Let $\boldsymbol{A}\in\mathbb{R}^{n\times m}$
> From $\boldsymbol{A}$ we can build two **symmetric** (and positive semidefinite) matrices:
> - the **left** one (size $n\times n$):
> $\boldsymbol{S}_{\text{left}}=\boldsymbol{A}\boldsymbol{A}^{\top}=\boldsymbol{U}\,\boldsymbol{\Lambda}\,\boldsymbol{U}^{\top}$
> - the **right** one (size $m\times m$):
> $\boldsymbol{S}_{\text{right}}=\boldsymbol{A}^{\top}\boldsymbol{A}=\boldsymbol{V}\,\boldsymbol{\Lambda}\,\boldsymbol{V}^{\top}$
> 
> $\boldsymbol{U}\in\mathbb{R}^{n\times n}$ contains eigenvectors of $\boldsymbol{A}\boldsymbol{A}^{\top}$(left singular vectors)
> $\boldsymbol{V}\in\mathbb{R}^{m\times m}$ contains eigenvectors of $\boldsymbol{A}^{\top}\boldsymbol{A}$ (right singular vectors)
> > [!note] ✍️
> > **therefore the SVD of **$\boldsymbol{A}$** is obtained by performing eigendecomposition of**
> > $\boldsymbol{A}\boldsymbol{A}^\top\quad \text{and} \quad\boldsymbol{A}^\top\boldsymbol{A}$,
> > **and pairing their eigenvectors via the same non-zero eigenvalues.**
> 
> - the** nonzero eigenvalues match **and are the squares of the singular values:
> $\boldsymbol{\Lambda}=\operatorname{diag}(\lambda_1,\ldots,\lambda_r,0,\ldots),
> \qquad
> \sigma_i=\sqrt{\lambda_i}$
> - Define
> $\boldsymbol{\Sigma}\in\mathbb{R}^{n\times m}$
> 
> $\begin{bmatrix}
> \sigma_1\\
> &\sigma_2\\
> &&\ddots\\
> &&&\sigma_r\\
> &&&&0
> \end{bmatrix}$
> (with zeros elsewhere). Then the **singular value decomposition** is:
> 
> $\boldsymbol{A}=\boldsymbol{U}\,\boldsymbol{\Sigma}\,\boldsymbol{V}^{\top}$

---
## Relation between eigendecomposition and SVD
**Eigendecomposition** works when a linear transformation admits a basis of invariant directions, allowing the transformation to be expressed as a change of basis, followed by pure scaling, and then the inverse change of basis. This requires independence of eigenvectors.
**SVD**, instead, does not rely on invariant directions. It expresses any linear transformation as a rotation (or reflection), followed by pure orthogonal scaling, followed by another rotation. Even when a transformation contains shear or other non-diagonalizable behavior, SVD isolates the scaling component by changing the input and output coordinate systems independently.

For a **square, symmetric, positive semi-definite matrix** (e.g. covariance matrices):
- left and right singular vectors coincide
- singular vectors = eigenvectors
- singular values = square roots of eigenvalues

In this case:
$\text{SVD} \equiv \text{eigendecomposition}$
### PCA connection
Principal Component Analysis (PCA) is based on the diagonalization of the **covariance matrix**, which is:
- square
- symmetric

Therefore:
- using eigendecomposition or SVD is mathematically equivalent
- in practice, **`prcomp` uses SVD** for numerical stability

---
## References
[SVD Visualized, Singular Value Decomposition explained | SEE Matrix , Chapter 3 #SoME2](https://www.youtube.com/watch?v=vSczTbgc8Rc)
