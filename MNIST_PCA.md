# MNIST_PCA

## Overview

| Field | Value |
|---|---|
| **Source** | OpenML |
| **Source URL** | https://www.openml.org/d/554 |
| **Domain** | General / Computer Vision |
| **Task** | Dimensionality reduction of handwritten digit images |
| **MLLO Type** | `DimensionalityReductionModel` |
| **Best Model** | PCA + t-SNE |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 70,000 images |
| **Input type** | Image — 28×28 grayscale, flattened to 784 features |
| **Output type** | Low-dimensional embedding (2D to 50D) |
| **Task** | Unsupervised dimensionality reduction |
| **Missing values** | None |
| **Original classes** | 10 (digits 0–9) — used for evaluation only, not training |

### What this task involves
MNIST digits are 784-dimensional vectors (one value per pixel). Dimensionality reduction compresses them into 2–50 dimensions while preserving structure. The goal is either:
- **Visualization:** Reduce to 2D so digit clusters are visually separable (t-SNE)
- **Feature extraction:** Reduce to 50D as preprocessing for a downstream classifier (PCA)

This dataset was added specifically to cover the `DimensionalityReductionModel` MLLO type.

---

## Best Model

| Field | Value |
|---|---|
| **Model** | PCA (reconstruction) + t-SNE (visualization) |
| **Model type** | Linear projection (PCA) / Non-linear embedding (t-SNE) |
| **Reference** | Scikit-learn documentation / van der Maaten & Hinton 2008 |
| **PCA evaluation** | ~85% explained variance at 50 components |
| **t-SNE evaluation** | Visually separable 2D clusters per digit class |
| **Framework** | Scikit-learn |

---

## MLLO Encoding

| MLLO Field | Value |
|---|---|
| `mllo_type` | `DimensionalityReductionModel` |
| `mllo_subtype` | `PrincipalComponentAnalysis` |
| `task_type` | `DimensionalityReduction` |
| `input_type` | `Image` |
| `output_type` | `LowDimensionalEmbedding` |

**Encoding gaps:**
- MLLO has no `LowDimensionalEmbedding` OutputType variant.
- Unsupervised evaluation metrics (reconstruction error, explained variance ratio, trustworthiness) are not capturable in current MLLO metadata.
- `DimensionalityReduction` may not be a supported TaskType in MLLO — requires verification.

---

## Links
- Dataset (OpenML): https://www.openml.org/d/554
- Original MNIST: http://yann.lecun.com/exdb/mnist/
- t-SNE paper: https://jmlr.org/papers/v9/vandermaaten08a.html
- Scikit-learn PCA: https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html
