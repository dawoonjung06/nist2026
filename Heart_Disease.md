# Heart_Disease

## Overview

| Field | Value |
|---|---|
| **Source** | UCI Machine Learning Repository |
| **Source URL** | https://archive.ics.uci.edu/dataset/45/heart+disease |
| **Domain** | Healthcare |
| **Task** | Binary classification — heart disease presence prediction |
| **MLLO Type** | `PolynomialModel` |
| **Best Model** | Logistic Regression |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 303 samples (Cleveland subset) |
| **Input type** | Tabular — 13 clinical features |
| **Output type** | Binary label (disease present / absent) |
| **Number of classes** | 2 |
| **Train / Val / Test split** | Typically 80/20 stratified split |
| **Missing values** | 6 samples with missing values (typically dropped) |

### Features

| Feature | Description |
|---|---|
| age | Age in years |
| sex | Sex (1 = male, 0 = female) |
| cp | Chest pain type (4 values) |
| trestbps | Resting blood pressure (mm Hg) |
| chol | Serum cholesterol (mg/dl) |
| fbs | Fasting blood sugar > 120 mg/dl (1 = true) |
| restecg | Resting ECG results |
| thalach | Maximum heart rate achieved |
| exang | Exercise-induced angina (1 = yes) |
| oldpeak | ST depression induced by exercise |
| slope | Slope of peak exercise ST segment |
| ca | Number of major vessels colored by fluoroscopy |
| thal | Thalassemia type |

---

## Best Model

| Field | Value |
|---|---|
| **Model** | Logistic Regression |
| **Model type** | Generalized Linear Model |
| **Reference** | UCI baseline |
| **Reported Accuracy** | ~85–88% |
| **Framework** | Scikit-learn |

---

## MLLO Encoding

| MLLO Field | Value |
|---|---|
| `mllo_type` | `PolynomialModel` |
| `mllo_subtype` | `LogisticRegression` |
| `task_type` | `BinaryClassification` |
| `input_type` | `TabularData` |
| `output_type` | `BinaryLabel` |

**Encoding gaps:** None — clean MLLO fit.

---

## Links
- Dataset: https://archive.ics.uci.edu/dataset/45/heart+disease
- Original study: Detrano et al., 1989
