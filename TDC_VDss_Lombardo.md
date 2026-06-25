# TDC.VDss_Lombardo

## Overview

| Field | Value |
|---|---|
| **Source** | Therapeutics Data Commons (TDC) |
| **Source URL** | https://tdcommons.ai/ |
| **Domain** | Drug Discovery |
| **Task** | Regression — steady-state volume of distribution prediction |
| **MLLO Type** | `PolynomialModel` |
| **Best Model** | Chemprop-RDKit |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 1,130 molecules |
| **Input type** | SMILES string / molecular graph + RDKit descriptors |
| **Output type** | Continuous value (volume in L/kg) |
| **Task** | Regression |
| **Train / Val / Test split** | TDC standard split (scaffold-based) |
| **Missing values** | None |
| **Provided by** | Lombardo et al. dataset |

### What this dataset measures
Volume of distribution at steady state (VDss) describes how widely a drug distributes throughout the body relative to its plasma concentration. A high VDss means the drug accumulates heavily in tissues. A low VDss means it stays mostly in the bloodstream. This affects how long a drug remains active and how it should be dosed. The dataset is compiled from published human pharmacokinetic studies.

---

## Best Model

| Field | Value |
|---|---|
| **Model** | Chemprop-RDKit |
| **Model type** | Message-Passing Neural Network with RDKit molecular descriptors |
| **Reference** | TDC Leaderboard 2024 |
| **Reported MAE** | ~0.447 log L/kg |
| **Framework** | PyTorch (Chemprop) |

---

## MLLO Encoding

| MLLO Field | Value |
|---|---|
| `mllo_type` | `PolynomialModel` |
| `mllo_subtype` | `MessagePassingNeuralNetwork` |
| `task_type` | `Regression` |
| `input_type` | `SMILES` |
| `output_type` | `ContinuousValue` |

**Encoding gaps:**
- Chemprop is a neural network, not a polynomial model. Assigned to `PolynomialModel` per project type mapping due to its linear output layer structure.
- MLLO has no `MolecularGraph` InputType variant. Encoded as `TabularData` as workaround.

---

## Links
- Dataset: https://tdcommons.ai/single_pred_tasks/adme/#vdss-lombardo-et-al
- Lombardo et al. paper: https://doi.org/10.1021/jm070827t
- Leaderboard: https://tdcommons.ai/benchmark/admet_group/overview/
