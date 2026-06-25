# Chronic_Kidney_Disease

## Overview

| Field | Value |
|---|---|
| **Source** | UCI Machine Learning Repository |
| **Source URL** | https://archive.ics.uci.edu/dataset/336/chronic+kidney+disease |
| **Domain** | Healthcare |
| **Task** | Binary classification — chronic kidney disease prediction |
| **MLLO Type** | `NonParametricModel` |
| **Best Model** | Random Forest |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 400 samples |
| **Input type** | Tabular — 24 features (mixed numeric + categorical) |
| **Output type** | Binary label (CKD / not CKD) |
| **Number of classes** | 2 (250 CKD, 150 not CKD) |
| **Train / Val / Test split** | Typically 80/20 stratified split |
| **Missing values** | Yes — significant; requires imputation before modeling |

### Features (24 total)

**Numeric (14):** Age, blood pressure, specific gravity, albumin, sugar, red blood cell count, white blood cell count, packed cell volume, serum creatinine, sodium, potassium, hemoglobin, blood glucose random, blood urea

**Categorical (10):** Red blood cells, pus cell, pus cell clumps, bacteria, hypertension, diabetes mellitus, coronary artery disease, appetite, pedal edema, anemia

---

## Best Model

| Field | Value |
|---|---|
| **Model** | Random Forest |
| **Model type** | Ensemble of Decision Trees |
| **Reference** | UCI baseline |
| **Reported Accuracy** | ~99% (with proper imputation) |
| **Framework** | Scikit-learn |

---

## MLLO Encoding

| MLLO Field | Value |
|---|---|
| `mllo_type` | `NonParametricModel` |
| `mllo_subtype` | `RandomForest` |
| `task_type` | `BinaryClassification` |
| `input_type` | `TabularData` |
| `output_type` | `BinaryLabel` |

**Encoding gaps:**
- High missing value rate — the preprocessing strategy (imputation method, dropped features) significantly affects results but is not capturable in current MLLO metadata fields.

---

## Links
- Dataset: https://archive.ics.uci.edu/dataset/336/chronic+kidney+disease
- Contributed by: L. Jerlin Rubini, Alagappa University, 2015
