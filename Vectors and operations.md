---

---
In linear algebra, vectors are defined as an ordered list of $n$ real numbers $(\in\mathbb{R})$ and usually denoted as $\mathbb{R}^n$
## Vector addition

$$
\boldsymbol{a} + \boldsymbol{b} =
\begin{bmatrix}a_1\\a_2\\a_3\end{bmatrix}+\begin{bmatrix}b_1\\b_2\\b_3\end{bmatrix}
=\begin{bmatrix}a_1 + b_1 \\a_2 + b_2 \\a_3 + b_3\end{bmatrix}
$$

---
## Scalar multiplication
$$
a \cdot \boldsymbol{b} =
a\cdot\begin{bmatrix}b_1\\b_2\\b_3\end{bmatrix}
=\begin{bmatrix}a\cdot b_1 \\a\cdot b_2 \\a \cdot b_3\end{bmatrix}
$$

---
## Dot product **(scalar Product)**
$$
\boldsymbol{a} \cdot \boldsymbol{b} =
\begin{bmatrix}a_1\\a_2\\a_3\end{bmatrix} \cdot \begin{bmatrix}b_1\\b_2\\b_3\end{bmatrix}
=a_1 \cdot b_1 + a_2 \cdot b_2 + a_3\cdot b_3
$$
The dot product returns a scalar and is useful to compute the angle between two vectors:
$$
\boldsymbol{a} \cdot \boldsymbol{b} =
\|\boldsymbol{a}\| \|\boldsymbol{b}\| \cos{\theta}
$$
Where $\|\boldsymbol{a}\|$ and $\|\boldsymbol{b}\|$ are the magnitudes (lengths) of the respective vectors.
***Note:**** Two vectors are orthogonal if and only if their dot product is zero*
> [!NOTE]
> **Notation**
> If the two vectors are indicated as matrices (column vectors), the dot product can also be indicated in the following form using matrix multiplication and transposition (pairwise dot products between columns)
> $\boldsymbol{a}^\top \boldsymbol{b}=\begin{bmatrix}a_1 & a_2 & \dots & a_n\end{bmatrix}\begin{bmatrix}b_1 \\b_2 \\\vdots \\b_n\end{bmatrix}=\sum_{i=1}^{n} a_i b_i$
> This is useful because when working with matrices, the dot product symbol should never be used, as it creates ambiguity.
> Sometimes it is used to imply matrix multiplications (composition of linear transformations) $\boldsymbol{A}\cdot \boldsymbol{B} = \boldsymbol{A}\boldsymbol{B}$ which is different from $\boldsymbol{A}^\top\boldsymbol{B}$ 


In python you can achieve dot product with `numpy.cdot(a, b)` 
> [!NOTE]
> **Vector magnitude**
> The magnitude of a vector is simply calculated with the Pitagora theorem
> $\|\boldsymbol{a}\| =\sqrt{a_1^2 + a_2^2+a_3^2}$
> This is also referred to as ***Euclidian distance*** or ***euclidean norm*** or $\ell^2$*** norm***.
> The exact notation is $\|\boldsymbol{a}\|_2$
> In python `numpy.linalg.norm(a, ord = 2)` 
> 
> Other common norms are:
> - ***absolute norm*** or **$\ell^1$ norm**
> $\|\boldsymbol{a}\|_1 =|a_1| + |a_2|+|a_3|$
> - ***uniform norm***, or ***sup norm*** or ***Chebyshev distance*** or ***maximum metric****,* or $\ell^\infty$ ***norm***
> $\|\boldsymbol{a}\|_\infty =\sqrt[\infty]{|a_1|^\infty + |a_2|^\infty + |a_3|^\infty}=\max(|a_1|, |a_2|, |a_3|)$
> 
> 

> [!NOTE]
> **Angle between vectors**
> $\cos{\theta}=\dfrac{\boldsymbol{a} \cdot \boldsymbol{b}}{\|\boldsymbol{a}\|\|\boldsymbol{b}\|}$
> which is the dot product of the two vectors normalized by their length


---
## Outer product
The **outer product** of two vectors $\boldsymbol{a}\in \mathbb{R}^m$ and $\boldsymbol{b}\in \mathbb{R}^n$ produces a matrix $\boldsymbol{C}\in \mathbb{R}^m\times n$:
$$
\boldsymbol{a}\boldsymbol{b}^\top=
\begin{bmatrix}
 a_1 \\
 a_2 \\
 \vdots
\end{bmatrix}
\begin{bmatrix}
 b_1 & b_2 & \dots
\end{bmatrix}
=
\begin{bmatrix}
 a_1 b_1 & a_1 b_2 & \dots \\
 a_2 b_1 & a_2 b_2 & \dots \\
 \vdots & \vdots & \ddots
\end{bmatrix}
$$
Outer products generate **rank‑1 matrices** and are fundamental in covariance matrices, PCA, and low‑rank factorizations.

---
## **Cross product (vector product)**
The cross product is mostly relevant to geometry and physics and less for statistics and ML.
$$
\boldsymbol{\vec{a} \times \vec{b}} =
\|\vec{a}\| \|\vec{b}\| \sin{\theta} \, \vec{n}
$$
$\vec{n}$ is a unit vector perpendicular to the plane containing $\vec{a}$ and $\vec{b}$

The cross product of two vectors is therefore a new vector perpendicular to the plane where the two vector lies and length equal to:
$$
\|\boldsymbol{a \times b} \| =
\|\boldsymbol{a}\| \|\boldsymbol{b}\| \sin{\theta}
$$
Differently from the dot product, the cross product is **non commutative**:
$\boldsymbol{a}\times \boldsymbol{b} = −(\boldsymbol{a}\times \boldsymbol{b})$
the order of the elements affects the direction of the resulting vector (right hand rule)

> [!NOTE]
> **Cross Product of Two Vectors Using Determinants**
> $\boldsymbol{a} =\begin{bmatrix}a_1 \\a_2 \\0\end{bmatrix},\qquad\boldsymbol{b} =\begin{bmatrix}b_1 \\b_2 \\0\end{bmatrix}$
> Note: $a_3$ and $b_3$ have been set to 0 to make a simpler example where the two original vectors lie on the i/j plane
> **let **$\boldsymbol{i}$**, **$\boldsymbol{j}$**, and **$\boldsymbol{k}$** be the canonical basis vectors**: a set of linearly independent vectors with one unit component and all others zero, used to define the standard coordinate system of the vector space
> $\boldsymbol{i} =\begin{bmatrix}1 \\ 0 \\ 0\end{bmatrix},\quad\boldsymbol{j} =\begin{bmatrix}0 \\ 1 \\ 0\end{bmatrix},\quad\boldsymbol{k} =\begin{bmatrix}0 \\ 0 \\ 1\end{bmatrix}$
> The cross product is computed via determinant expansion:
> $\boldsymbol{a} \times \boldsymbol{b}=\begin{vmatrix}\boldsymbol{i} & \boldsymbol{j} & \boldsymbol{k} \\a_1 & a_2 & 0 \\b_1 & b_2 & 0\end{vmatrix} = \boldsymbol{i}\begin{vmatrix}a_2 & 0 \\b_2 & 0\end{vmatrix}-\boldsymbol{j}\begin{vmatrix}a_1 & 0 \\b_1 & 0\end{vmatrix}+\boldsymbol{k}\begin{vmatrix}a_1 & a_2 \\b_1 & b_2\end{vmatrix} = \left( a_1 b_2 - a_2 b_1 \right)\boldsymbol{k}$
> In this example the $2 \times 2$ determinants multiplying $\boldsymbol{i}$ and $\boldsymbol{j}$ are **zero** because their columns are **linearly dependent, h**ence, those submatrices are **singular**, and their determinants vanish.


**References**

---
[https://medium.com/@ebimsv/mastering-linear-algebra-part-2-fundamental-concepts-of-linear-algebra-5216daafe203](https://medium.com/@ebimsv/mastering-linear-algebra-part-2-fundamental-concepts-of-linear-algebra-5216daafe203)
