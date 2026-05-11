PCA can be defined as the eigenvalue of the covariance matrix.
Can also be computed equivalently with singolar value decomposition

---
Covariance matrix
$\text{cov}(x,y)=\dfrac{1}{n}\displaystyle\sum_{i=1}^n(x_i-\bar{x})(y_i-\bar{y})$
If we start from a $\boldsymbol{X} \in \mathbb{R}^{n\times p}$ matrix with n observations and p features, and features are aleready 0 centered (first internal step when performing PCA), than covariance matrix can be simply calculated as
$\text{cov}(x,y)=\dfrac{1}{n}\displaystyle\sum_{i=1}^nx_iy_i$
which becomes:
$\boldsymbol\Sigma=\dfrac{1}{n}\boldsymbol{X}^\top\boldsymbol{X}$
or $n-1$ for sample covariance
> [!NOTE]
> **Proof:**
> Take a $\boldsymbol{X} \in \mathbb{R}^{n \times p}$ matrix with $n=3$ observations and $p=2$ features. $x$ and $y$ identifies the two features of each observations. Could be also coords on a 2D plane. It leds for an easier notation for this example rather than using $x_{1,1}, x_{1,2}$
> Assume the features are already mean-centered.
>
> $$
> \boldsymbol{X} =\begin{bmatrix}x_1 & y_1 \\
> x_2 & y_2 \\
> x_3 & y_3\end{bmatrix},\qquad\text{with }x_1+x_2+x_3 = 0,\;y_1+y_2+y_3 = 0
> $$
>
> $$
> \boldsymbol{X}^\top \boldsymbol{X}=\begin{bmatrix}x_1 & x_2 & x_3 \\
> y_1 & y_2 & y_3\end{bmatrix}\begin{bmatrix}x_1 & y_1 \\x_2 & y_2 \\
> x_3 & y_3\end{bmatrix}\implies
> $$
>
> $$
> \boldsymbol{X}^\top \boldsymbol{X}=\begin{bmatrix}x_1^2 + x_2^2 + x_3^2&x_1y_1 + x_2y_2 + x_3y_3\\
> [6pt]x_1y_1 + x_2y_2 + x_3y_3&y_1^2 + y_2^2 + y_3^2\end{bmatrix}\implies
> $$
>
> $$
> \boldsymbol\Sigma=\dfrac{1}{3} \boldsymbol{X}^\top \boldsymbol{X}=\begin{bmatrix}\frac{1}{3}\sum x_i^2&\frac{1}{3}\sum x_i y_i\\
> [6pt]\frac{1}{3}\sum x_i y_i&\frac{1}{3}\sum y_i^2\end{bmatrix}=\begin{bmatrix}\text{Var}(\boldsymbol{x}) & \text{Cov}(\boldsymbol{x},\boldsymbol{y})\\
> \text{Cov}(\boldsymbol{x},\boldsymbol{y}) & \text{Var}(\boldsymbol{y})\end{bmatrix}
> $$
> 
> Note: $\boldsymbol\Sigma$ is conventionally used for the **covariance matrix** which is different from the concept of **Summation** $\sum$

Note: covariance matrices are symmetric matrices
$\boldsymbol{\Sigma}=\boldsymbol{\Sigma}^\top$
Symmetric matrices have the following properties:
- All eigenvalues are real
- All eigenvector are orthogonal


![Covariance matrix geometry](images/image%202.png)

The eigenvectors and eigenvalues describe the two main covariance components
![PCA eigenvectors](images/image%203.png)
![PCA projection](images/image%204.png)
> [!NOTE]
> **Computing PCA with eigendecomposition in R**
> ```bash
> ## =========================
> ## Data (example)
> ## =========================
> set.seed(1)
> X <- matrix(rnorm(100 * 5), ncol = 5)
> colnames(X) <- paste0("gene", 1:5)
> 
> center <- TRUE
> scale. <- TRUE
> 
> ## Standardize like prcomp(scale.=TRUE)
> Xcs <- scale(X, center = center, scale = scale.)
> n <- nrow(Xcs)
> p <- ncol(Xcs)
> 
> ## =========================
> ## 1) Manual PCA via eigen(Cov)
> ## =========================
> # Sample covariance of standardized data
> S <- cov(Xcs)  # equals t(Xcs) %*% Xcs / (n - 1)
> 
> eig <- eigen(S)
> 
> # Eigenvalues (variances of PCs) and eigenvectors (loadings)
> lambda <- eig$values          # length p
> V <- eig$vectors              # p x p, columns are eigenvectors
> 
> # Loadings: columns are PCs, rows are variables
> loadings_eig <- V
> 
> # Scores (PC coordinates of samples): Xcs %*% loadings
> scores_eig <- Xcs %*% loadings_eig  # n x p
> 
> # Variance explained
> var_explained_eig <- lambda
> pve_eig <- lambda / sum(lambda)     # proportion variance explained
> cum_pve_eig <- cumsum(pve_eig)
> 
> ## =========================
> ## 2) Manual PCA via SVD (prcomp-style)
> ## =========================
> sv <- svd(Xcs)  # Xcs = U D V^T
> 
> U <- sv$u                 # n x p (or n x n, but here n>p so n x p effectively used)
> D <- sv$d                 # length p
> V_svd <- sv$v             # p x p
> 
> # Loadings are V (same meaning as eigenvectors of covariance)
> loadings_svd <- V_svd
> 
> # Scores are Xcs %*% V  (equivalently U %*% diag(D))
> scores_svd1 <- Xcs %*% loadings_svd
> scores_svd2 <- U %*% diag(D)
> 
> # Variances of PCs: eigenvalues = D^2 / (n-1)
> lambda_svd <- (D^2) / (n - 1)
> pve_svd <- lambda_svd / sum(lambda_svd)
> cum_pve_svd <- cumsum(pve_svd)
> 
> ## =========================
> ## 3) Compare to prcomp()
> ## =========================
> pc <- prcomp(X, center = center, scale. = scale.)
> 
> # prcomp outputs:
> # pc$rotation : loadings (p x p)
> # pc$x        : scores (n x p)
> # pc$sdev     : standard deviations of PCs
> #             : variances = pc$sdev^2
> 
> loadings_prcomp <- pc$rotation
> scores_prcomp <- pc$x
> lambda_prcomp <- pc$sdev^2
> pve_prcomp <- lambda_prcomp / sum(lambda_prcomp)
> 
> ## =========================
> ## 4) Handle sign ambiguity + check equality
> ## =========================
> # PCA loadings are defined up to sign flips per PC.
> # Align eigen loadings to prcomp by matching column signs.
> align_signs <- function(A, B) {
>   # A and B: same dim, columns are PCs
>   s <- sign(colSums(A * B))  # sign that maximizes agreement
>   s[s == 0] <- 1
>   sweep(A, 2, s, `*`)
> }
> 
> loadings_eig_aligned <- align_signs(loadings_eig, loadings_prcomp)
> loadings_svd_aligned <- align_signs(loadings_svd, loadings_prcomp)
> 
> scores_eig_aligned <- Xcs %*% loadings_eig_aligned
> scores_svd_aligned <- Xcs %*% loadings_svd_aligned
> 
> ## Numeric checks (should be ~0)
> cat("Max |loadings_eig - prcomp|:", max(abs(loadings_eig_aligned - loadings_prcomp)), "\n")
> cat("Max |loadings_svd - prcomp|:", max(abs(loadings_svd_aligned - loadings_prcomp)), "\n")
> cat("Max |lambda_eig - prcomp|:", max(abs(lambda - lambda_prcomp)), "\n")
> cat("Max |pve_eig - prcomp|:", max(abs(pve_eig - pve_prcomp)), "\n")
> cat("Max |scores_eig - prcomp|:", max(abs(scores_eig_aligned - scores_prcomp)), "\n")
> 
> ## =========================
> ## 5) Print a compact summary
> ## =========================
> out <- data.frame(
>   PC = paste0("PC", 1:p),
>   var = lambda_prcomp,
>   pve = pve_prcomp,
>   cum_pve = cumsum(pve_prcomp)
> )
> print(out)
> 
> ```
> 
## References

---
[https://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/](https://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/)
