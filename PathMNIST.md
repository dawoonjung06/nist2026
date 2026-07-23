# PathMNIST

## Overview
- **Source:** MedMNIST — https://medmnist.com/
- **Domain:** Medical imaging — colon pathology
- **Task:** Multi-class classification (9 tissue types)
- **Data modality:** Pathology microscope images
- **Image size:** 28×28 pixels (also available in 64, 128, 224)
- **License:** CC BY 4.0

## Dataset Size
- Total: ~107,180 samples
- Train: 89,996 / Validation: 10,004 / Test: 7,180

## Models and Performance
| Model | AUC | ACC |
|---|---|---|
| ResNet-50 (28) | 0.990 | 0.911 |
| ResNet-18 (28) | 0.983 | 0.907 |
| auto-sklearn | 0.934 | 0.716 |
| AutoKeras | 0.959 | 0.834 |
| Google AutoML Vision | 0.944 | 0.728 |

## MLLO Encoding
- **MLLO Model Type:** ArtificialNeuralNetwork → ConvolutionalNeuralNetwork
- **Selected model for encoding:** ResNet-50 (28)
- **Performance metric:** AUC, ACC
- **Dataset split:** Train / Validation / Test****

file link: https://medmnist.com/
