# PathMNIST

## Overview

| Field | Value |
|---|---|
| **Source** | MedMNIST |
| **Source URL** | https://medmnist.com/ |
| **Domain** | Medical Imaging |
| **Task** | Multi-class classification of colon pathology images |
| **MLLO Type** | `ArtificialNeuralNetwork` |
| **Best Model** | ResNet-50 |

---

## Dataset Details

| Field | Value |
|---|---|
| **Dataset size** | 107,180 images |
| **Input type** | Image — 28×28 RGB |
| **Output type** | Categorical label (9 classes) |
| **Number of classes** | 9 colon tissue types |
| **Train / Val / Test split** | 89,996 / 10,004 / 7,180 |
| **Missing values** | None |

### Classes
1. Adipose tissue
2. Background
3. Debris
4. Lymphocytes
5. Mucus
6. Smooth muscle
7. Normal colon mucosa
8. Cancer-associated stroma
9. Colorectal adenocarcinoma epithelium

---

## Best Model

| Field | Value |
|---|---|
| **Model** | ResNet-50 |
| **Model type** | Convolutional Neural Network |
| **Reference** | He et al., 2016 — Deep Residual Learning for Image Recognition |
| **Reported AUC** | ~0.990 |
| **Framework** | PyTorch / torchvision |

---

## MLLO Encoding

| MLLO Field | Value |
|---|---|
| `mllo_type` | `ArtificialNeuralNetwork` |
| `mllo_subtype` | `ConvolutionalNeuralNetwork` |
| `task_type` | `MultiClassClassification` |
| `input_type` | `Image` |
| `output_type` | `CategoricalLabel` |

**Encoding gaps:** None — clean MLLO fit.

---

## Links
- Dataset: https://medmnist.com/
- Paper: https://arxiv.org/abs/2110.14795
- Leaderboard: https://paperswithcode.com/dataset/pathmnist
