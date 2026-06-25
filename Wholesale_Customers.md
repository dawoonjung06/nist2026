# Wholesale_Customers

## Overview

| Field | Value |
|---|---|
| **Source** | UCI Machine Learning Repository |
| **Source URL** | https://archive.ics.uci.edu/dataset/292/wholesale+customers |
| **Domain** | General / Retail |
| **Task** | Clustering — discover customer segments by spending pattern |
| **MLLO Type** | `ClusteringModel` |
| **Best Model** | K-Means (k=3) |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 440 samples |
| **Input type** | Tabular — 6 continuous spend features |
| **Output type** | Cluster assignment (no ground truth labels) |
| **Task** | Unsupervised clustering |
| **Missing values** | None |

### Features

| Feature | Description |
|---|---|
| Fresh | Annual spending on fresh products (monetary units) |
| Milk | Annual spending on milk products |
| Grocery | Annual spending on grocery products |
| Frozen | Annual spending on frozen products |
| Detergents_Paper | Annual spending on detergents and paper products |
| Delicatessen | Annual spending on delicatessen products |

Two additional categorical columns (Channel, Region) are available but excluded from clustering features.

### Why this dataset
This dataset was added specifically to cover the `ClusteringModel` MLLO type. K-Means on spending data is a textbook unsupervised learning task with a clean, interpretable result (e.g. "bulk buyers", "fresh-focused", "mixed-spend" customer segments).

---

## Best Model

| Field | Value |
|---|---|
| **Model** | K-Means (k=3) |
| **Model type** | Centroid-based clustering |
| **Reference** | UCI baseline / standard practice |
| **Evaluation** | Silhouette score ~0.45, elbow method at k=3 |
| **Framework** | Scikit-learn |

---

## MLLO Encoding

| MLLO Field | Value |
|---|---|
| `mllo_type` | `ClusteringModel` |
| `mllo_subtype` | `KMeans` |
| `task_type` | `Clustering` |
| `input_type` | `TabularData` |
| `output_type` | `ClusterAssignment` |

**Encoding gaps:**
- No ground truth labels exist — MLLO has no intrinsic evaluation metric support. Silhouette score and elbow criterion cannot be encoded in current MLLO metadata.
- `ClusterAssignment` may not be a supported OutputType in MLLO — requires verification.

---

## Links
- Dataset: https://archive.ics.uci.edu/dataset/292/wholesale+customers
- Contributed by: Margarida Cardoso, ISCTE-IUL, 2014
