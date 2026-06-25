# Breast_Cancer_Wisconsin

## Overview

| Field | Value |
|---|---|
| **Source** | UCI Machine Learning Repository |
| **Source URL** | https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic |
| **Domain** | Healthcare |
| **Task** | Binary classification — tumor malignancy prediction |
| **MLLO Type** | `NonParametricModel` |
| **Best Model** | SVM (RBF kernel) |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 569 samples |
| **Input type** | Tabular — 30 numeric features |
| **Output type** | Binary label (Malignant / Benign) |
| **Number of classes** | 2 (357 benign, 212 malignant) |
| **Train / Val / Test split** | Typically 80/20 stratified split |
| **Missing values** | None |

### Features
Features are computed from a digitized image of a fine needle aspirate (FNA) of a breast mass. They describe characteristics of the cell nuclei present in the image. For each nucleus, 10 measurements are captured (mean, standard error, and worst/largest value = 30 features total):

- Radius, Texture, Perimeter, Area, Smoothness
- Compactness, Concavity, Concave points, Symmetry, Fractal dimension

---

## Best Model

| Field | Value |
|---|---|
| **Model** | SVM (RBF kernel) |
| **Model type** | Support Vector Machine |
| **Reference** | UCI baseline |
| **Reported Accuracy** | ~97–98% |
| **Framework** | Scikit-learn |

---

## MLLO Encoding

| MLLO Field | Value |
|---|---|
| `mllo_type` | `NonParametricModel` |
| `mllo_subtype` | `SupportVectorMachine` |
| `task_type` | `BinaryClassification` |
| `input_type` | `TabularData` |
| `output_type` | `BinaryLabel` |

**Encoding gaps:** None — clean MLLO fit.

---

## Links
- Dataset: https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic
- Original paper: https://doi.org/10.1117/12.148698
