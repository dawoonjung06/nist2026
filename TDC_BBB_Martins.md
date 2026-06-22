# TDC.BBB_Martins

## Overview
- **Source:** Therapeutics Data Commons (TDC) — https://tdcommons.ai/benchmark/admet_group/07bbb/
- **Domain:** Drug discovery — ADMET
- **Task:** Binary classification
- **What it predicts:** Whether a drug molecule can cross the blood-brain barrier
- **Unit:** %
- **Dataset split:** Scaffold split
- **Metric:** AUROC

## Dataset Size
- Total: 1,975 molecules

## Models and Performance
| Rank | Model | AUROC |
|---|---|---|
| 1 | MiniMol | 0.924 ± 0.003 |
| 2 | CFA | 0.920 ± 0.006 |
| 3 | MapLight | 0.916 ± 0.001 |
| 8 | Lantern RADR Random Forest | 0.908 ± 0.002 |
| 10 | Lantern RADR SVM | 0.905 ± 0.007 |
| 17 | Chemprop-RDKit | 0.869 ± 0.027 |

## MLLO Encoding
- **MLLO Model Type:** ArtificialNeuralNetwork
- **Selected model for encoding:** MiniMol (rank 1)
- **Performance metric:** AUROC
- **Dataset split:** Scaffold

## DATASET
from tdc.single_pred import ADMET
data = ADMET(name='BBB_Martins')
df = data.get_data()
df.to_csv('BBB_Martins.csv', index=False)

