# TDC.DILI

## Overview

| Field | Value |
|---|---|
| **Source** | Therapeutics Data Commons (TDC) |
| **Source URL** | https://tdcommons.ai/ |
| **Domain** | Drug Discovery |
| **Task** | Binary classification — drug-induced liver injury prediction |
| **MLLO Type** | `NonParametricModel` |
| **Best Model** | MapLight + GNN |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 475 molecules |
| **Input type** | SMILES string / molecular graph |
| **Output type** | Binary label (DILI-positive / DILI-negative) |
| **Number of classes** | 2 |
| **Train / Val / Test split** | TDC standard split (scaffold-based) |
| **Missing values** | None |

### What this dataset measures
Drug-induced liver injury (DILI) is one of the leading causes of drug withdrawal from the market and failure in clinical trials. This dataset contains drugs labeled as DILI-positive or DILI-negative based on FDA adverse event data and clinical literature. Predicting DILI early in drug development can save significant cost and prevent patient harm.

---

## Best Model

| Field | Value |
|---|---|
| **Model** | MapLight + GNN |
| **Model type** | Graph Neural Network with bioactivity features |
| **Reference** | TDC Leaderboard 2024 |
| **Reported AUROC** | ~0.866 |
| **Framework** | PyTorch Geometric |

---

## MLLO Encoding

| MLLO Field | Value |
|---|---|
| `mllo_type` | `NonParametricModel` |
| `mllo_subtype` | `GradientBoostedTree` |
| `task_type` | `BinaryClassification` |
| `input_type` | `SMILES` |
| `output_type` | `BinaryLabel` |

**Encoding gaps:**
- MapLight+GNN is a graph neural network — architecturally closer to `ArtificialNeuralNetwork`. Assigned to `NonParametricModel` per project type mapping.
- MLLO has no `MolecularGraph` InputType variant. Encoded as `TabularData` as workaround.

---

## Links
- Dataset: https://tdcommons.ai/single_pred_tasks/tox/#dili-drug-induced-liver-injury
- Leaderboard: https://tdcommons.ai/benchmark/admet_group/overview/
