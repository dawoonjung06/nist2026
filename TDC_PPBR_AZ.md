# TDC.PPBR_AZ

## Overview

| Field | Value |
|---|---|
| **Source** | Therapeutics Data Commons (TDC) |
| **Source URL** | https://tdcommons.ai/ |
| **Domain** | Drug Discovery |
| **Task** | Regression — plasma protein binding rate prediction |
| **MLLO Type** | `PolynomialModel` |
| **Best Model** | Chemprop-RDKit |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 1,614 molecules |
| **Input type** | SMILES string / molecular graph + RDKit descriptors |
| **Output type** | Continuous value (% bound to plasma proteins) |
| **Task** | Regression |
| **Train / Val / Test split** | TDC standard split (scaffold-based) |
| **Missing values** | None |
| **Provided by** | AstraZeneca |

### What this dataset measures
When a drug enters the bloodstream, a large fraction of it binds to plasma proteins (mainly albumin). Only the unbound fraction is pharmacologically active. A drug that is 99% protein-bound has only 1% free to exert its effect. This property directly affects dosing, drug interactions, and efficacy. The dataset contains plasma protein binding rates measured by AstraZeneca.

---

## Best Model

| Field | Value |
|---|---|
| **Model** | Chemprop-RDKit |
| **Model type** | Message-Passing Neural Network with RDKit molecular descriptors |
| **Reference** | TDC Leaderboard 2024 |
| **Reported MAE** | ~7.5% |
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
- Dataset: https://tdcommons.ai/single_pred_tasks/adme/#ppbr-az
- Chemprop paper: https://doi.org/10.1021/acs.jcim.9b00237
- Leaderboard: https://tdcommons.ai/benchmark/admet_group/overview/
