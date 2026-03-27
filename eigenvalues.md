## Eigenvalue Gap Analysis

We analyze the sorted eigenvalue gaps of the normalized Laplacian across datasets. This provides insight into spectral degeneracy (repeated eigenvalues) and near-degeneracy (clusters of very small gaps).

### Amazon-Ratings

![Amazon eigengaps](amazon_eigengap_hist.png)

Amazon-Ratings exhibits a large number of *exact or near-zero eigenvalue gaps*, indicating repeated eigenvalues and strong spectral degeneracy.  
This implies that many eigenvectors correspond to the same frequency, making the spectral basis highly non-unique.

---

### Roman-Empire

![Roman eigengaps](roman_eigengap_hist.png)

Roman-Empire does not show exact repetitions, but contains a significant number of *extremely small eigenvalue gaps*, which are below our deflation threshold.  
These form tight spectral clusters that are effectively indistinguishable numerically and can be treated as a single mode.

---

### Tolokers

![Tolokers eigengaps](tolokers_eigengap_hist.png)

Tolokers presents a smoother spectrum with fewer extreme degeneracies, though small gaps are still present.  
This represents an intermediate regime between well-separated and highly clustered spectra.

---

### Minesweeper

![Minesweeper eigengaps](minesweeper_eigengap_hist.png)

Minesweeper shows a relatively well-behaved spectrum, with fewer near-zero gaps and more gradual variation across frequencies.

---

**Our method remains robust**, as it does not rely on a strictly unique or well-separated eigenvalues, operating instead in a deflated representation.
