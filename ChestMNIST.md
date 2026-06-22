# ChestMNIST

## Overview
- **Source:** MedMNIST — https://medmnist.com/
- **Domain:** Medical imaging — chest X-ray
- **Task:** Multi-label classification (14 disease labels)
- **Data modality:** X-Ray images
- **Image size:** 28×28 pixels (also available in 64, 128, 224)
- **License:** CC BY 4.0

## Dataset Size
- Total: ~112,120 samples
- Train: 78,468 / Validation: 11,219 / Test: 22,433

## Models and Performance
| Model | AUC | ACC |
|---|---|---|
| ResNet-50 (224) | 0.773 | 0.948 |
| ResNet-18 (224) | 0.773 | 0.947 |
| Google AutoML Vision | 0.778 | 0.948 |
| auto-sklearn | 0.649 | 0.779 |
| AutoKeras | 0.742 | 0.937 |

## MLLO Encoding
- **MLLO Model Type:** ArtificialNeuralNetwork → ConvolutionalNeuralNetwork
- **Selected model for encoding:** ResNet-18 (28)
- **Performance metric:** AUC, ACC
- **Dataset split:** Train / Validation / Test

- LINK: https://medmnist.com/
