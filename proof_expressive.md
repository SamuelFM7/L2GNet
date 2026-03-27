# Expressiveness of L2G-Net

**Proposition.** The family of linear operators representable by L2G-Net strictly contains those representable by global spectral filters $g(\mathbf{L})$ and by polynomial filters.

**Proof.** We establish three inclusions.

---

## Part 1: Polynomial filters $\subset$ global spectral filters $g(\mathbf{L})$

A polynomial filter of degree $K$ computes

$$\sum_{k=0}^{K} \alpha_k \mathbf{L}^k \mathbf{x} = \mathbf{U} p(\boldsymbol{\Lambda}) \mathbf{U}^\top \mathbf{x},$$

where $p(\lambda) = \sum_k \alpha_k \lambda^k$. This is a global spectral filter with $g = p$. Since spectral filters permit arbitrary functions $g$ of the eigenvalues (not just polynomials), polynomial filters form a strict subset. For example, a filter that equals 1 on a single eigenvalue and 0 on all others is realizable by a spectral filter but not by any polynomial of degree less than $n-1$.

On a finite graph with $n$ distinct eigenvalues, any function on the spectrum can be interpolated by a polynomial of degree at most $n-1$ (cf. Wang and Zhang, 2022, Section 2.2). Therefore, on a fixed graph, the algebra of polynomials in $\mathbf{L}$ and the class of operators $\mathbf{U} g(\boldsymbol{\Lambda}) \mathbf{U}^\top$ coincide. We use "$g(\mathbf{L})$" to denote this class throughout. $\square$

---

## Part 2: Global spectral filters $g(\mathbf{L}) \subseteq$ L2G-Net

Consider a graph $\mathcal{G} \in \mathcal{F}(L, \{\mathcal{G}_i\}, k)$. By Theorem 3.1, the GFT admits the Cauchy factorization

$$\mathbf{U}^\top = \mathbf{D}(\boldsymbol{\lambda}, \tilde{\boldsymbol{\lambda}}_{K-1}) \cdots \mathbf{D}(\tilde{\boldsymbol{\lambda}}_1, \tilde{\boldsymbol{\lambda}}_0) \mathbf{U}_0^\top,$$

where $\mathbf{U}_0 = \mathrm{blkdiag}(\mathbf{U}_1, \ldots, \mathbf{U}_m)$ collects the base subgraph GFTs and each $\mathbf{D}$ is a Cauchy factor.

In L2G-Net (Eq. 10), at each hierarchical level $r$ and subgraph pair $p$, a learnable spectral filter $g_{r,p}(\boldsymbol{\lambda}_{r,p})$ is applied before the Cauchy merge. Setting all intermediate filters to the identity, i.e., $g_{r,p}(\lambda) = 1$ for all $\lambda$, $r = 0, \ldots, L-1$, and all $p$, the forward transform $\mathbf{U}(\Phi)^\top$ reduces exactly to $\mathbf{U}^\top$ by Theorem 3.1.

The L2G-Net output then becomes

$$\mathbf{X}_{\mathrm{out}} = \mathbf{U} g_\theta(\boldsymbol{\Lambda}) \mathbf{U}^\top \mathbf{X},$$

which is a standard global spectral filter. Since the identity is within the parameterization of L2G-Net's local filters, every global spectral filter is realizable. $\square$

---

## Part 3: Global spectral filters $g(\mathbf{L}) \subsetneq$ L2G-Net (strict containment)

We show that L2G-Net can represent operators that no global spectral filter $g(\mathbf{L})$ can express, by exhibiting an explicit counterexample.

### Setup

Consider a graph $\mathcal{G} \in \mathcal{F}(1, \{\mathcal{G}_1, \mathcal{G}_2\}, k)$ with $k \geq 1$, i.e., two subgraphs $\mathcal{G}_1$, $\mathcal{G}_2$ connected by at least one bridge edge. With one level of hierarchy, the L2G-Net forward transform is:

$$\mathbf{U}(\Phi)^\top = g_1(\boldsymbol{\Lambda}) \cdot \mathbf{D} \cdot \mathrm{blkdiag}\bigl(g_{0,1}(\boldsymbol{\Lambda}_1),\; g_{0,2}(\boldsymbol{\Lambda}_2)\bigr) \cdot \mathbf{U}_0^\top,$$

where $\mathbf{D}$ is the product of Cauchy factors for the bridge edges and $g_1$ acts on the merged spectrum. Define $\mathbf{F}_{\mathrm{loc}} := \mathrm{blkdiag}(g_{0,1}(\boldsymbol{\Lambda}_1), g_{0,2}(\boldsymbol{\Lambda}_2))$.

The full L2G-Net operator is:

$$\mathbf{T}_{\mathrm{L2G}} = \mathbf{U}\, g_\theta(\boldsymbol{\Lambda})\, g_1(\boldsymbol{\Lambda})\, \mathbf{D}\, \mathbf{F}_{\mathrm{loc}}\, \mathbf{U}_0^\top.$$

A global spectral filter takes the form:

$$\mathbf{T}_{\mathrm{GFT}} = \mathbf{U}\, h(\boldsymbol{\Lambda})\, \mathbf{U}^\top = \mathbf{U}\, h(\boldsymbol{\Lambda})\, \mathbf{D}\, \mathbf{U}_0^\top,$$

where the last equality uses Theorem 3.1 with identity local filters.

### Necessary condition for collapse

For $\mathbf{T}_{\mathrm{L2G}} = \mathbf{T}_{\mathrm{GFT}}$ to hold for some $h$, we require:

$$g_\theta(\boldsymbol{\Lambda})\, g_1(\boldsymbol{\Lambda})\, \mathbf{D}\, \mathbf{F}_{\mathrm{loc}} = h(\boldsymbol{\Lambda})\, \mathbf{D}.$$

Let $f(\boldsymbol{\Lambda}) := g_\theta(\boldsymbol{\Lambda}) g_1(\boldsymbol{\Lambda})$ (a diagonal matrix). Since $\mathbf{D}$ is orthogonal (being a product of orthogonal Cauchy-like matrices), we can right-multiply by $\mathbf{D}^\top$ to obtain:

$$f(\boldsymbol{\Lambda})\, \mathbf{D}\, \mathbf{F}_{\mathrm{loc}}\, \mathbf{D}^\top = h(\boldsymbol{\Lambda}).$$

Since $h(\boldsymbol{\Lambda})$ is diagonal, a necessary condition is:

$$\mathbf{D}\, \mathbf{F}_{\mathrm{loc}}\, \mathbf{D}^\top \text{ is diagonal.} \qquad (\star)$$

### Explicit counterexample: two singleton subgraphs

Consider $n_1 = n_2 = 1$: two isolated nodes connected by a single edge of weight $w > 0$. The base subgraphs are singletons with trivial GFTs ($\mathbf{U}_0 = \mathbf{I}_2$). The Laplacian of the disconnected graph is $\mathbf{L}_0 = \mathbf{0}$, and adding the bridge edge gives

$$\mathbf{L} = w \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix},$$

with eigenvalues $0$ and $2w$, and eigenvectors

$$\mathbf{U} = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}.$$

By Theorem 3.1, $\mathbf{U}^\top = \mathbf{D} \cdot \mathbf{U}_0^\top = \mathbf{D} \cdot \mathbf{I}_2$, so the Cauchy factor is

$$\mathbf{D} = \mathbf{U}^\top = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}.$$

This is a nontrivial orthogonal matrix (not diagonal, not a permutation). Now let $\mathbf{F}_{\mathrm{loc}} = \mathrm{diag}(a, b)$ with $a \neq b$. Then:

$$\mathbf{D}\, \mathbf{F}_{\mathrm{loc}}\, \mathbf{D}^\top = \frac{1}{2} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} a & 0 \\ 0 & b \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} = \frac{1}{2} \begin{pmatrix} a+b & a-b \\ a-b & a+b \end{pmatrix}.$$

The off-diagonal entry is $\frac{a-b}{2} \neq 0$ whenever $a \neq b$. Therefore, condition $(\star)$ fails, and the L2G-Net operator $\mathbf{T}_{\mathrm{L2G}}$ cannot be expressed as any global spectral filter $g(\mathbf{L})$.

Since this construction uses a valid member of $\mathcal{F}(1, \{\mathcal{G}_1, \mathcal{G}_2\}, 1)$ and a non-constant local filter (which is within L2G-Net's parameterization), we conclude that the inclusion is strict. $\square$

---

## Summary

Combining Parts 1–3:

$$\text{Polynomial filters} \;\subset\; g(\mathbf{L}) \;\subsetneq\; \text{L2G-Net}.$$

Therefore, L2G-Net strictly generalizes global spectral filtering by enabling region-dependent spectral responses that cannot be collapsed into a single function of the Laplacian.

---

## Remark 1 (Generality beyond the counterexample)

The 2-node example is a minimal proof of strict inclusion. The phenomenon extends to arbitrary graphs: since Cauchy factors arising from bridge edges are dense orthogonal matrices with all nonzero entries (a defining property of Cauchy-like matrices, cf. Definition 2.2), the conjugation $\mathbf{D}\, \mathbf{F}_{\mathrm{loc}}\, \mathbf{D}^\top$ is non-diagonal whenever $\mathbf{F}_{\mathrm{loc}}$ is not proportional to the identity.

## Remark 2 (Intuition)

A global spectral filter $g(\mathbf{L})$ applies the same spectral response uniformly across the entire graph. L2G-Net breaks this constraint by applying different spectral responses to different subgraphs before merging via Cauchy factors, producing operators that cannot be represented as any single function of the Laplacian. The partition structure provides the additional degrees of freedom.
