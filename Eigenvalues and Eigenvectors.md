In linear algebra, a **square matrix** can be interpreted as a **linear transformation** of space. **Eigenvectors** are special vectors that, under this transformation, **do not change direction**, but are only **scaled**.
The corresponding **eigenvalue** quantifies how much the eigenvector is stretched or compressed.
Note: in linear transformations for an eigenvalue, there are infinite eigenvectors along the same axis so it would be better to refer to spans (vector sub-space) rather than vectors. 
## **Definition**
Given a $\boldsymbol{A} \in \mathbb{R}^{n \times n}$ square matrix. A non‑zero vector $\vec{\boldsymbol{v}} \in \mathbb{R}^n$ is an **eigenvector** of $\boldsymbol{A}$ if:
$\boldsymbol{A}\vec{\boldsymbol{v}}=\lambda\vec{\boldsymbol{v}}$
where $\lambda \in \mathbb{R}$ is the corresponding **eigenvalue**.
Geometrically:
- $\boldsymbol{v}$ defines an invariant direction of the transformation
- $\lambda$ is the scaling factor along that direction, the sign informs about the orientation flipping

Along each eigenvector direction, **all scalar multiples** of $\boldsymbol{v}$ are also eigenvectors, forming a **1‑dimensional subspace**.

---
## **Number of eigenvalues**
A matrix $\boldsymbol{A} \in \mathbb{R}^{n \times n}$ can have:
- up to $n$ eigenvalues

**Note:** Each distinct eigenvalue defines exactly one eigenspace, but **eigenspaces can have different dimensions**.
The dimension of the eigenspace $E$ associated with $\lambda$ (or equivalently the maximum number of linearly independent eigenvectors associated with $\lambda$), is referred to as the eigenvalue's **geometric multiplicity**
$\gamma_A(\lambda)=n-\text{rank}(\boldsymbol{A}-\lambda\boldsymbol{I})$
### Examples
- A **shear**:

  $$
  \boldsymbol{S_1} =
  \begin{bmatrix}
  1 & 1 \\
  0 & 1
  \end{bmatrix}
  $$

  It has only one eigenvalue $\lambda=1$ and the dimension of the eigenspace is $\mathbb{R}^1$ (a line).
- A **scale**:

  $$
  \boldsymbol{S_2} =
  \begin{bmatrix}
  2 & 0 \\
  0 & 2
  \end{bmatrix}
  $$

  It has only one eigenvalue $\lambda=2$ and the dimension of the eigenspace is $\mathbb{R}^2$ (a space) because every vector in the 2d space preserves its orientation.
- A **rotation**:

  $$
  \boldsymbol{R} =
  \begin{bmatrix}
  0 & -1 \\
  1 & 0
  \end{bmatrix}
  $$

  It has no real eigenvalues and no real eigenspaces (only the null space $\mathbb{R}^0$ which is discarded by definition) since no real direction is preserved.

---
## **Zero eigenvalues**
An eigenvalue $\lambda = 0$ implies:
$\boldsymbol{A}\boldsymbol{v} = \boldsymbol{0}$
This means that the transformation **collapses** the eigenvector to zero.
**Implications:**
- the matrix is **singular **(non-invertible)
- the transformation reduces dimensionality
- the rank of the matrix is lower than $n$

---
## **How to find eigenvalues and eigenvectors**
Starting from the eigenvalue equation:
$\boldsymbol{A}\boldsymbol{v} = \lambda\boldsymbol{v}$
we rewrite it as:
$(\boldsymbol{A} - \lambda\boldsymbol{I})\boldsymbol{v} = \boldsymbol{0}$
where $\boldsymbol{I}$ is the identity matrix.
A non‑zero vector can be mapped to zero **only if the matrix is singular**, therefore:
$\det(\boldsymbol{A} - \lambda\boldsymbol{I}) = 0$
This equation is called the **characteristic equation**, and solving it yields the **eigenvalues**.
Once an eigenvalue $\lambda$ is known, the corresponding eigenvectors are obtained by solving:
$(\boldsymbol{A} - \lambda\boldsymbol{I})\boldsymbol{v} = \boldsymbol{0}$
This identifies a **subspace** (the *eigenspace*), not a single vector.
### **Python**
In Python, eigenvalues and eigenvectors can be computed as:
`numpy.linalg.eig(A)`
Notes:
- eigenvectors are returned **unit‑normalized**
- the **sign of eigenvectors is arbitrary**

```python
# a shear transformation with one eigenvalue (geometric multiplicity) and a eigenspace 1D
>>> S = np.array([[1, 1],
				   0, 1]])
>>> np.linalg.eig(S)

EigResult(eigenvalues=array([1., 1.]),
		  eigenvectors=array([[ 1.00000000e+00, -1.00000000e+00],
							  [ 0.00000000e+00,  2.22044605e-16]]))
```
NumPy returns eigenvalues with algebraic multiplicity and is forced to output $n$ vectors for an $\boldsymbol{A}\in \mathbb{R}^{n \times n}$ matrix, even when the matrix has fewer independent eigenvectors.
### **Algebraic vs geometric multiplicity**

For an eigenvalue $\lambda$:
- **Algebraic multiplicity (AM)**
= how many times $\lambda$ appears as a root of the **characteristic polynomial**
- **Geometric multiplicity (GM)**
= dimension of the **eigenspace**
= number of **linearly independent eigenvectors** for $\lambda$

Always:
$1 \;\le\; \text{GM} \;\le\; \text{AM}$
> [!NOTE]
> **Example:** $\text{GM} = 2$, $\text{AM} = 2$
> $\boldsymbol{A}=\begin{pmatrix}2 & 0 \\0 & 2\end{pmatrix}$
> $\det(\boldsymbol{A}-\lambda \boldsymbol{I})=0 \implies \det\begin{pmatrix}2-\lambda & 0 \\0-\lambda & 2-\lambda\end{pmatrix}=(2-\lambda)^2=0$
> $\implies (2-\lambda)(2-\lambda)=0 \implies \begin{cases}\lambda - 2 = 0 \\ \lambda - 2 = 0\end{cases}$
> $\lambda = 2 \quad \text{with algebraic multiplicity } 2$
> 
> $(\boldsymbol{A}-2\boldsymbol{I})\vec{\boldsymbol{v}}=\boldsymbol{0}\quad \implies 0\vec{\boldsymbol{v}}=0 \implies \vec{\boldsymbol{v}} \in \mathbb{R}^2$
> $\text{Geometric multiplicity} = \dim(\mathbb{R}^2) = 2$
> 

> [!NOTE]
> **Example:** $\text{GM} = 1$, $\text{AM} = 2$
> $\boldsymbol{B}=\begin{pmatrix}2 & 1 \\0 & 2\end{pmatrix}$
> $\det(\boldsymbol{B}-\lambda \boldsymbol{I})=0 \implies\det\begin{pmatrix}2-\lambda & 1 \\0 & 2-\lambda\end{pmatrix}=(2-\lambda)^2=0$
> $\lambda = 2 \quad \text{with algebraic multiplicity } 2$
> $(\boldsymbol{B}-2\boldsymbol{I})\vec{\boldsymbol{v}}=\begin{pmatrix}0 & 1 \\0 & 0\end{pmatrix}\vec{\boldsymbol{v}}=\boldsymbol{0}$
> $\vec{v_2} = 0$
> $\boldsymbol{v}=x\begin{pmatrix}1 \\0\end{pmatrix}\quad \Rightarrow \quad\text{Geometric multiplicity} = 1$


---
## **Algebraic properties**
Let ${\lambda_i}$ be the eigenvalues of $\boldsymbol{A}$:
- **Trace**:
$\mathrm{tr}(\boldsymbol{A}) = \sum_i \lambda_i$
- **Determinant**:
$\det(\boldsymbol{A}) = \prod_i \lambda_i$

These relations hold regardless of whether the matrix is diagonalizable.

---
## Closed-form solution for $2 \times 2$ matrices
For a $2 \times 2$ matrix:
$\boldsymbol{A} = \begin{bmatrix} a & b \\ c & d \end{bmatrix}$
Define:
$m = \dfrac{\lambda_1+\lambda_2}{2}=\dfrac{\mathrm{tr}(\boldsymbol{A})}{2} = \dfrac{a + d}{2}$
$p = \lambda_1\cdot\lambda_2=\det(\boldsymbol{A}) = ad - bc$
The eigenvalues are:
$\lambda_{1,2} = m \pm \sqrt{m^2 - p}$
> [!NOTE]
> **Example: pure 90° rotation in 2D and complex eigenvalues**
> Consider a **pure 90° rotation** in 2D (counter-clockwise):
>
> $$
> \boldsymbol{R} =
> \begin{bmatrix}
> 0 & -1 \\
> 1 & 0
> \end{bmatrix}
> $$
>
> This transformation maps:
> - the x-axis to the y-axis
> - the y-axis to the negative x-axis
> 
> It preserves lengths and angles, but **no real direction remains invariant**.
> We solve the characteristic equation:
>
> $$
> \det(\boldsymbol{R} - \lambda \boldsymbol{I}) = 0 \implies \det
> \begin{bmatrix}
> -\lambda & -1 \\
> 1 & -\lambda
> \end{bmatrix}
> = \lambda^2 + 1 = 0
> $$
>
> Therefore, the matrix has **no real eigenvalues** and **no real eigenvectors**.
> $\lambda_{1,2}=\pm \,i$
> 
## References

---
[Eigenvectors and eigenvalues | Chapter 14, Essence of linear algebra](https://www.youtube.com/watch?v=PFDu9oVAE-g)
[https://medium.com/@ebimsv/mastering-linear-algebra-part-6-eigenvalues-and-eigenvectors-7927cab9a0ad](https://medium.com/@ebimsv/mastering-linear-algebra-part-6-eigenvalues-and-eigenvectors-7927cab9a0ad)
