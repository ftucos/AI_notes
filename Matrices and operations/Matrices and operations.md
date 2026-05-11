---

---
In linear algebra, a **matrix** is a rectangular array of real numbers arranged in rows and columns. A matrix with *m* rows and *n* columns belongs to  $\mathbb{R}^{m\times n}$

$$
\boldsymbol{A} = \begin{bmatrix}
 a_{11} & a_{12} & \dots & a_{1n} \\
 a_{21} & a_{22} & \dots & a_{2n} \\
 \vdots & \vdots & \ddots & \vdots \\
 a_{m1} & a_{m2} & \dots & a_{mn}
\end{bmatrix}
$$

Matrices generalize vectors (which are matrices with one column or one row) and are used to represent **linear transformations**, **systems of equations**, and **bilinear operations:**

---
## Matrix addition
Two matrices can be added **only if they have the same shape**:

$$
\boldsymbol{A} + \boldsymbol{B} =
\begin{bmatrix}
 a_{11} & a_{12} \\
 a_{21} & a_{22}
\end{bmatrix}
+
\begin{bmatrix}
 b_{11} & b_{12} \\
 b_{21} & b_{22}
\end{bmatrix}
=
\begin{bmatrix}
 a_{11}+b_{11} & a_{12}+b_{12} \\
 a_{21}+b_{21} & a_{22}+b_{22}
\end{bmatrix}
$$

---
## Scalar multiplication
A matrix can be multiplied by a scalar $a \in \mathbb{R}$ by multiplying every entry:

$$
a\cdot\boldsymbol{B} = a\begin{bmatrix}
 b_{11} & b_{12} \\
 b_{21} & b_{22}
\end{bmatrix}
=
\begin{bmatrix}
 a b_{11} & a b_{12} \\
 a b_{21} & a b_{22}
\end{bmatrix}
$$
Scalar multiplication rescales the linear transformation represented by the matrix.

---
## Hadamard product (**elementwise multiplication**)
If $\boldsymbol{A}\in \mathbb{R}^{m\times n}$ and $\boldsymbol{B}\in \mathbb{R}^{m\times n}$, then $\boldsymbol{C}\in \mathbb{R}^{m\times n}$:
$\boldsymbol{A} \odot \boldsymbol{B} = \boldsymbol{B}\odot \boldsymbol{A} = \boldsymbol{C}$
$\begin{bmatrix}2 & 3 & 1\\0 & 8 & -2\end{bmatrix}\odot\begin{bmatrix}3 & 1 & 4\\7 & 9 & 5\end{bmatrix}=\begin{bmatrix}2\times 3 & 3\times 1 & 1\times 4\\0\times 7 & 8\times 9 & -2\times 5\end{bmatrix}=\begin{bmatrix}6 & 3 & 4\\0 & 72 & -10\end{bmatrix}$

---
## Matrix multiplication
Matrix multiplication is **not element‑wise** and is defined only when the inner dimensions match.
If $\boldsymbol{A}\in \mathbb{R}^{m\times n}$ and $\boldsymbol{B}\in \mathbb{R}^{n\times p}$, then $\boldsymbol{C}\in \mathbb{R}^{m\times p}$
with elements:
$c_{ij} = \displaystyle\sum_{k=1}^{n} a_{ik} b_{kj}$
each new element of the resulting matrix is the dot product of the rows $n$ of $\boldsymbol{A}$ with each matching the column $n$ of $\boldsymbol{B}$

$$
\underbrace{
\begin{bmatrix}
\color{red}{a_{11}} & \color{red}{a_{12}} \\
\color{orange}{a_{21}} & \color{orange}{a_{22}} \\
\color{yellow}{a_{31}} & \color{yellow}{a_{32}}
\end{bmatrix}
}_{3\times2}
\;
\underbrace{
\begin{bmatrix}
\color{violet}{b_{11}} & \color{blue}{b_{12}} & \color{cyan}{b_{13}} \\
\color{violet}{b_{21}} & \color{blue}{b_{22}} & \color{cyan}{b_{23}}
\end{bmatrix}
}_{2\times3}
=
\underbrace{
\begin{bmatrix}
\color{red}{a_{11}}\color{violet}{b_{11}} + \color{red}{a_{12}}\color{violet}{b_{21}} &
\color{red}{a_{11}}\color{blue}{b_{12}} + \color{red}{a_{12}}\color{blue}{b_{22}} &
\color{red}{a_{11}}\color{cyan}{b_{13}} + \color{red}{a_{12}}\color{cyan}{b_{23}}
\\[6pt]
\color{orange}{a_{21}}\color{violet}{b_{11}} + \color{orange}{a_{22}}\color{violet}{b_{21}} &
\color{orange}{a_{21}}\color{blue}{b_{12}} + \color{orange}{a_{22}}\color{blue}{b_{22}} &
\color{orange}{a_{21}}\color{cyan}{b_{13}} + \color{orange}{a_{22}}\color{cyan}{b_{23}}
\\[6pt]
\color{yellow}{a_{31}}\color{violet}{b_{11}} + \color{yellow}{a_{32}}\color{violet}{b_{21}} &
\color{yellow}{a_{31}}\color{blue}{b_{12}} + \color{yellow}{a_{32}}\color{blue}{b_{22}} &
\color{yellow}{a_{31}}\color{cyan}{b_{13}} + \color{yellow}{a_{32}}\color{cyan}{b_{23}}
\end{bmatrix}
}_{3\times3}
$$
Conceptually, matrix multiplication corresponds to the **composition of linear maps**.
[Matrix Multiplication as combination of linear transformations](Matrix%20Multiplication%20as%20combination%20of%20linear%20transformations.md)
***Note:**** Matrix multiplication is ****associative**** but ****not commutative***:
$(\boldsymbol{A}\boldsymbol{B})\boldsymbol{C}= \boldsymbol{A}(\boldsymbol{B}\boldsymbol{C})$
$\boldsymbol{A}\boldsymbol{B}\neq \boldsymbol{B}\boldsymbol{A}$
see: 
[Matrix Multiplications for equations](Matrix%20Multiplications%20for%20equations.md)

---
## Matrix–vector product
A matrix applied to a vector produces a new vector:

$$
\boldsymbol{A}\boldsymbol{x} =
\begin{bmatrix}
 a_{11} & a_{12} \\
 a_{21} & a_{22}
\end{bmatrix}
\begin{bmatrix}
 x_1 \\
 x_2
\end{bmatrix}
=
\begin{bmatrix}
 a_{11}x_1 + a_{12}x_2 \\
 a_{21}x_1 + a_{22}x_2
\end{bmatrix}
$$
This represents a **linear transformation** of the vector space (rotation, scaling, shearing, projection) 

---
## Transpose
The transpose of a matrix swaps rows and columns:
$\boldsymbol{A}^\top=(a_{ji})$

$$
\begin{bmatrix}
 a_{11} & a_{12} \\
 a_{21} & a_{22}
\end{bmatrix}^\top
=
\begin{bmatrix}
 a_{11} & a_{21} \\
 a_{12} & a_{22}
\end{bmatrix}
$$
Properties:
${(\boldsymbol{A}^\top)}^\top = \boldsymbol{A}$
$(\boldsymbol{A}\boldsymbol{B})^\top = \boldsymbol{B}^\top \boldsymbol{A}^\top$

---
## Identity matrix
The **identity matrix** acts as the neutral element of multiplication:

$$
\boldsymbol{I}_n =
\begin{bmatrix}
 1 & 0 & \dots \\
 0 & 1 & \dots \\
 \vdots & \vdots & \ddots
\end{bmatrix}
$$
$\boldsymbol{A}\boldsymbol{I}=\boldsymbol{I}\boldsymbol{A}=\boldsymbol{A}$

---
## Linear dependence
A set of vectors (rows or columns of a matrix) are said to be linearly dependent if at least one of the vectors can be expressed as a linear combination of others. In simpler terms, this means that some vectors do not add new directions in the vector space; they are redundant.
![Linearly dependent vectors](../images/image%201.png)
### Rank of a matrix
The rank of a matrix is equal to the number of linearly independent rows (or columns) in it. Hence, it cannot have more than its number of rows and columns. For example, if we consider the identity matrix of order $3 \times 3$, all its rows (or columns) are linearly independent, and hence its rank is 3.

If a matrix is **rank-1  **it means it can be constructed by the outer product of two vectors
$\boldsymbol{A}=\boldsymbol{v}\boldsymbol{w}^\top$

---
## Determinant of a Matrix
The **determinant** is a scalar associated with a **square matrix** and measures volume scaling and invertibility.
For a $2\times 2$ matrix:

$$
\det(\boldsymbol{A}) =
\begin{vmatrix}
 a & b \\
 c & d
\end{vmatrix}
= ad - bc
$$
### Interpretation:
For a $2 \times 2$ matrix $\boldsymbol{A}$, the absolute value of the determinant $|\det(\boldsymbol{A})|$ represents the **area scaling factor** of the associated linear transformation.
Geometrically, it corresponds to the area of the **parallelogram spanned by the images of the canonical basis vectors** $[1, 0]$ and $[0, 1]$ after applying the transformation $\boldsymbol{A}$.
If $\det(\boldsymbol{A}) = 2$  then the area of **every planar region** (e.g. squares, polygons etc) is expanded by a factor of 2 under this transformation.
### Orientation
- $\det(\boldsymbol{A}) > 0$: orientation is preserved
- $\det(\boldsymbol{A}) < 0$: orientation is reversed (reflection)
- $\det(\boldsymbol{A}) =0$ → the matrix is **singular **(non-invertible) → after the transformation the two basis axis becomes linearly dependent (collapse on the same axis and the area of the parallelogram becomes 0)
This means that for a matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$ if $\det(\boldsymbol{A}) =0$ then $\operatorname{rank}(\boldsymbol{A})<n$

---
## Inverse matrix
Non every matrix is invertible. Inverting a matrix can conceptualized as the transformation that reverts another transformation
$\boldsymbol{A}\boldsymbol{A}^{-1}=\boldsymbol{I}$** **
If a transformation collpases one or more dimensions (reduces the rank, $\det{(\boldsymbol{A})}=0$) than it is not possible to revert back that transformation. Therefore only squares matrices can be invertible.
For $2 \times 2$ matrices:

$$
\boldsymbol{A}^{-1} = \dfrac{1}{\det(\boldsymbol{A})}
\begin{bmatrix}
 d & -b \\
 -c & a
\end{bmatrix}
$$

---
## Matrix Division
$\boldsymbol{A}/\boldsymbol{B}=\boldsymbol{A}\boldsymbol{B}^{-1}$
It can be conceptualized as applying an undo (inverse) transformation.
This is useful for solving equations:
$\boldsymbol{A}\boldsymbol{X}=\boldsymbol{B} \implies \boldsymbol{X}=\boldsymbol{B}\boldsymbol{A}^{-1}$

---
## Common types of matrices
- **Diagonal matrix**: usually refers to a square matrix with non‑zero elements only on the diagonal. If all the values in the diagonal are the same, than it becomes a **scalar matrix** because it's transformation only rescales objects and it is equivalent to scalar multiplication. scalar
Those matrices apply scaling along each axis.
The identity matrix is a special case of  matrix. 
    - Eigenvalues are the diagonal entries
    - Eigenvectors are the **canonical basis vectors**
- **Symmetric matrix**: $\boldsymbol{A}=\boldsymbol{A}^\top$
    - Always **diagonalizable**
    - All eigenvalues are orthogonal
- **Orthogonal matrix**: $\boldsymbol{A}\boldsymbol{A}^\top=\boldsymbol{I}$  
Those matrix apply **rigid rotation and reflection **but not scaling of the space. Therefore **determinant** of an orthogonal matrix is** +/- 1.**
Having a determinant of 1 does not imply its a orthogonal matrix (you can have shearing preserving surface/volume). Orthogonal matrix also require that the dotproduct of their columns is 0 (columns form an **orthonormal basis**), and each column has unit norm (no scaling).
All eigenvalues have magnitude 1, can have complex eigenvalues
- **Upper / lower triangular**: zeros below / above the diagonal

---
## Trace
The **trace** of a square matrix is the sum of diagonal elements:
$\operatorname{tr}(\boldsymbol{A})= \sum_{i=1}^{n} a_{ii}= a_{11} + a_{22} + \dots + a_{nn}$
Useful properties:
- $\operatorname{tr}(\boldsymbol{AB})=\operatorname{tr}(\boldsymbol{BA})$
- The trace of a matrix equals the sum of its eigenvalues


### **References**

---
[https://medium.com/@ebimsv/mastering-linear-algebra-part-3-matrices-in-linear-algebra-35861c3f77af](https://medium.com/@ebimsv/mastering-linear-algebra-part-3-matrices-in-linear-algebra-35861c3f77af)
