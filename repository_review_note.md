# Repository Review Note

**Date:** 2026-06-25  
**Purpose:** Identify publicly available datasets and pre-trained models suitable for MLLO demonstration across 5 targeted model types.

---

## Repositories Reviewed

### 1. MedMNIST
- **URL:** https://medmnist.com/
- **Type:** Curated medical imaging benchmark suite
- **What it contains:** 12 standardized 2D and 3D medical image datasets derived from real clinical sources (pathology slides, X-rays, retinal scans, etc.), all pre-split into train/val/test and resized to 28×28
- **Why reviewed:** Provides clean, reproducible image classification benchmarks with published leaderboard results — ideal for `ArtificialNeuralNetwork` type coverage
- **Datasets selected:** PathMNIST, ChestMNIST
- **Datasets considered but not selected:** RetinaMNIST (regression task, fewer published baselines), OrganMNIST (too similar to PathMNIST)

---

### 2. Therapeutics Data Commons (TDC)
- **URL:** https://tdcommons.ai/
- **Type:** Drug discovery and biomedical ML benchmark hub
- **What it contains:** 66+ datasets covering ADMET properties (absorption, distribution, metabolism, excretion, toxicity), molecular property prediction, and drug-target interaction — with leaderboards and standardized splits
- **Why reviewed:** Best publicly available source for drug discovery ML benchmarks with reproducible leaderboard models. Covers regression and classification on molecular inputs.
- **Datasets selected:** BBB_Martins, DILI, Clearance_Hepatocyte_AZ, PPBR_AZ, VDss_Lombardo
- **Datasets considered but not selected:** CYP2C9_Veith (too correlated with DILI), hERG (cardiac toxicity — similar task type to DILI)

---

### 3. UCI Machine Learning Repository
- **URL:** https://archive.ics.uci.edu/
- **Type:** General-purpose ML dataset archive (1000+ datasets)
- **What it contains:** Tabular datasets spanning classification, regression, clustering across healthcare, finance, biology, and other domains. Well-established baselines exist for most datasets.
- **Why reviewed:** Most reliable source for tabular healthcare datasets with known baselines for `NonParametricModel` and `PolynomialModel` types. Also covers `ClusteringModel` tasks.
- **Datasets selected:** Breast Cancer Wisconsin, Heart Disease, Chronic Kidney Disease, Wholesale Customers
- **Datasets considered but not selected:** Diabetes (Pima Indians) — overlaps too much with Heart Disease in feature type; Iris — too simple, no meaningful MLLO encoding

---

### 4. OpenML
- **URL:** https://www.openml.org/
- **Type:** Open ML experiment and dataset sharing platform
- **What it contains:** Thousands of datasets with attached experiment results, reproducible pipelines, and community benchmarks
- **Why reviewed:** Best source for `DimensionalityReductionModel` coverage — MNIST with documented PCA/t-SNE pipelines is canonical and widely reproducible
- **Datasets selected:** MNIST (for PCA/t-SNE dimensionality reduction pipeline)
- **Datasets considered but not selected:** Fashion-MNIST (same structure as MNIST, no added MLLO diversity)

---

### 5. Kaggle
- **URL:** https://www.kaggle.com/datasets
- **Type:** Competition and community dataset platform
- **What it contains:** Large variety of real-world datasets with community notebooks and competition leaderboards
- **Why reviewed:** Considered as supplementary source, particularly for clustering and association rule tasks
- **Outcome:** Not used for final candidate selection — UCI datasets provided cleaner baselines for the same domains, and Kaggle datasets often lack reproducible published model references needed for MLLO encoding

---

### 6. Papers with Code
- **URL:** https://paperswithcode.com/datasets
- **Type:** ML paper and benchmark tracker
- **What it contains:** Datasets linked to published papers with state-of-the-art leaderboards and code
- **Why reviewed:** Cross-reference tool to verify that selected datasets have published best models with citable references — used as a validation step rather than a primary source
- **Outcome:** Used to confirm leaderboard models for MedMNIST and TDC datasets

---

## Review Outcome

| Source | Datasets Selected | MLLO Types Covered |
|---|---|---|
| MedMNIST | 2 | ArtificialNeuralNetwork |
| TDC | 5 | ArtificialNeuralNetwork, NonParametricModel, PolynomialModel |
| UCI | 4 | NonParametricModel, PolynomialModel, ClusteringModel |
| OpenML | 1 | DimensionalityReductionModel |
| Kaggle | 0 | — |
| Papers with Code | 0 (validation only) | — |

**Total datasets selected:** 12  
**MLLO types covered:** 5 of 6 (`AssociationRuleModel` excluded — see candidates note)
