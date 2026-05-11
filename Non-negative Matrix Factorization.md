In linear algebra and data analysis, **Non-negative Matrix Factorization (NMF)** is a matrix factorization technique designed for **additive, parts-based representations**.
Given a **non-negative matrix** $\boldsymbol{A}\in\mathbb{R}_{\ge 0}^{p\times n}$
where you can think of $n$ as the number of samples and $p$ the number of features
$\boldsymbol{A} \;\approx\; \boldsymbol{W}\boldsymbol{H}$
where:
- $\boldsymbol{W}\in\mathbb{R}_{\ge 0}^{p\times k}$ is the **dictionary/patterns** which describes how much each latent dimension $k$ (in transcriptiomics can be metagene or a regulon) activates each feature $p$ (gene)
- $\boldsymbol{H}\in\mathbb{R}_{\ge 0}^{k\times n}$ is the **activations** matrix describing the activity of each latent dimension for each samples. By multipling the $h_i$ column by
- all entries are **non-negative**
- $k$ is $k \ll \min(n,p)$. $k$ can be chosen with the elbow method or other heuristics. The approximation error for $\boldsymbol{A}$ decreases monotonically with the number latent dimensions chosen.

![NMF components](images/image%205.png)
NMF expresses therefore each observation as a **sum of non-negative components**:
$\boldsymbol{x}i \;\approx\; \boldsymbol{W}h_i$
- reconstruction is **purely additive**
- **subtraction and sign cancellation are forbidden**
- high interpretability. $\boldsymbol{W}$ clearly describes what each metafeature adds

---
## Optimization problem
NMF is **not a closed-form decomposition**.
It is solved by minimizing a cost function:
$$
\min_{\boldsymbol{W},\boldsymbol{H}\ge 0}
\;\;
\|\boldsymbol{X}-\boldsymbol{W}\boldsymbol{H}\|^2
$$
or alternative divergences (e.g. KL divergence).
Key consequences:
- the solution is **not unique**
- results depend on **initialization**
- convergence is to a **local minimum**
- component order has **no intrinsic meaning**

---
## Comparison with SVD / PCA

| Property | PCA / SVD | NMF |
| --- | --- | --- |
| Signs allowed | positive & negative | **only positive** |
| Orthogonality | yes | no |
| Uniqueness | yes (up to sign) | **no** |
| Reconstruction | additive + subtractive | **additive only** |
| Interpretation | global directions | **parts-based** |

- PCA components can **cancel each other**
- NMF components can **only accumulate**

---
## When NMF is a good choice
NMF is particularly suitable when:
- data are naturally **non-negative**
    - gene expression counts
    - pixel intensities
    - topic frequencies
- interpretability matters
- signals are expected to be **additive**
- components correspond to **parts or programs**

---
## When NMF is a bad choice
NMF struggles when:
- negative correlations are meaningful
- signals repress or cancel each other
- reproducibility of components is critical

In these cases, PCA / SVD-based methods are often preferable.

---
## Relation to PCA intuition
- **PCA**: *What orthogonal directions best explain variance?*
- **NMF**: *What positive building blocks can reconstruct the data?*

PCA separates **directions**.
NMF separates **recurrent components**.
