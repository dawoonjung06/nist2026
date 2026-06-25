# ChestMNIST

## Overview

| Field | Value |
|---|---|
| **Source** | MedMNIST |
| **Source URL** | https://medmnist.com/ |
| **Domain** | Medical Imaging |
| **Task** | Multi-label classification of chest X-ray diseases |
| **MLLO Type** | `ArtificialNeuralNetwork` |
| **Best Model** | ResNet-18 |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 112,120 images |
| **Input type** | Image — 28×28 grayscale |
| **Output type** | Multiple binary labels (14 conditions simultaneously) |
| **Number of labels** | 14 thoracic conditions |
| **Train / Val / Test split** | 78,468 / 11,219 / 22,433 |
| **Missing values** | None |

### Labels (14 thoracic conditions)
Atelectasis, Cardiomegaly, Effusion, Infiltration, Mass, Nodule, Pneumonia, Pneumothorax, Consolidation, Edema, Emphysema, Fibrosis, Pleural Thickening, Hernia

---

## Best Model

| Field | Value |
|---|---|
| **Model** | ResNet-18 |
| **Model type** | Convolutional Neural Network |
| **Reference** | He et al., 2016 — Deep Residual Learning for Image Recognition |
| **Reported AUC** | ~0.773 (mean AUC across 14 labels) |
| **Framework** | PyTorch / torchvision |

---

## MLLO Encoding

| MLLO Field | Value |
|---|---|
| `mllo_type` | `ArtificialNeuralNetwork` |
| `mllo_subtype` | `ConvolutionalNeuralNetwork` |
| `task_type` | `MultiLabelClassification` |
| `input_type` | `Image` |
| `output_type` | `MultipleCategoricalLabels` |

**Encoding gaps:**
- `MultiLabelClassification` is not a supported OutputType in MLLO — encoded as `MultiClassClassification` as workaround. This loses the semantics of multiple simultaneous labels per image.

---

## Links
- Dataset: https://medmnist.com/
- Paper: https://arxiv.org/abs/2110.14795
- Original NIH ChestX-ray14: https://nihcc.app.box.com/v/ChestXray-NIHCC
- Leaderboard: https://paperswithcode.com/dataset/chestmnist
