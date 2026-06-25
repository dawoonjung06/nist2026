# Dataset & Model Candidates Note

**Date:** 2026-06-25  
**Purpose:** Document the 12 selected dataset candidates, their best-known models, MLLO type assignments, and the rationale for selection and exclusion of the 6th MLLO type.

---

## MLLO Model Types Targeted (5 of 6)

| # | MLLO Type | Selected | Reason |
|---|---|---|---|
| 1 | ArtificialNeuralNetwork | ✅ | Strong coverage in medical imaging and drug discovery |
| 2 | NonParametricModel | ✅ | Dominant model family in tabular healthcare and drug data |
| 3 | PolynomialModel | ✅ | Strong baselines in UCI healthcare datasets |
| 4 | ClusteringModel | ✅ | Covered by Wholesale Customers (UCI) |
| 5 | DimensionalityReductionModel | ✅ | Covered by MNIST PCA pipeline (OpenML) |
| 6 | AssociationRuleModel | ❌ | No suitable transaction-format dataset in medical/drug domains |

**Why AssociationRuleModel was excluded:**  
Apriori and FP-Growth require transaction-format data (e.g. market baskets, diagnosis co-occurrence logs). None of the domains covered here — medical imaging, drug discovery, tabular healthcare — produce this format naturally. Adding a forced retail dataset would break domain cohesion. This type is deferred to a future iteration.

---

## Selected Candidates (12 Datasets)

---

### 1. PathMNIST
- **Source:** MedMNIST — https://medmnist.com/
- **Domain:** Medical Imaging
- **Task:** Multi-class classification of colon pathology images (9 tissue types)
- **Input type:** 28×28 RGB images
- **Output type:** Categorical label (9 classes)
- **Dataset size:** 107,180 images
- **Best model:** ResNet-50
- **MLLO type:** `ArtificialNeuralNetwork`
- **Why selected:** Clean benchmark with published leaderboard, image input covers ANN/CNN use case well, colon pathology is clinically relevant
- **Notes:** Pre-split train/val/test available directly from MedMNIST API

---

### 2. ChestMNIST
- **Source:** MedMNIST — https://medmnist.com/
- **Domain:** Medical Imaging
- **Task:** Multi-label classification of chest X-ray images (14 thoracic conditions simultaneously)
- **Input type:** 28×28 grayscale images
- **Output type:** Multiple binary labels (14 conditions)
- **Dataset size:** 112,120 images
- **Best model:** ResNet-18
- **MLLO type:** `ArtificialNeuralNetwork`
- **Why selected:** Introduces multi-label classification — a distinct and clinically important task type not covered by PathMNIST
- **Encoding gap:** MLLO has no `MultiLabelClassification` OutputType variant — encoded as `MultiClassClassification` as workaround

---

### 3. TDC.BBB_Martins
- **Source:** Therapeutics Data Commons — https://tdcommons.ai/
- **Domain:** Drug Discovery
- **Task:** Binary classification — does a drug molecule penetrate the blood-brain barrier?
- **Input type:** SMILES string / molecular graph
- **Output type:** Binary label (penetrates / does not penetrate)
- **Dataset size:** 1,975 molecules
- **Best model:** MiniMol
- **MLLO type:** `ArtificialNeuralNetwork`
- **Why selected:** Blood-brain barrier penetration is one of the most important ADMET properties in CNS drug development; well-studied benchmark
- **Encoding gap:** MLLO has no `MolecularGraph` InputType — encoded as `TabularData` as workaround

---

### 4. TDC.DILI
- **Source:** Therapeutics Data Commons — https://tdcommons.ai/
- **Domain:** Drug Discovery
- **Task:** Binary classification — does a drug cause drug-induced liver injury (DILI)?
- **Input type:** SMILES string / molecular graph
- **Output type:** Binary label
- **Dataset size:** 475 molecules
- **Best model:** MapLight + GNN
- **MLLO type:** `NonParametricModel`
- **Why selected:** DILI is a leading cause of drug withdrawal — high clinical impact. Covers a different toxicity prediction task from BBB.
- **Encoding gap:** MapLight+GNN is a graph neural network; encoded as NonParametricModel per project type mapping. SMILES InputType gap applies.

---

### 5. TDC.Clearance_Hepatocyte_AZ
- **Source:** Therapeutics Data Commons — https://tdcommons.ai/
- **Domain:** Drug Discovery
- **Task:** Regression — how fast does the liver clear a drug (hepatocyte clearance rate)?
- **Input type:** SMILES string / molecular graph
- **Output type:** Continuous value (clearance rate)
- **Dataset size:** 1,020 molecules
- **Best model:** RFStacker (stacked Random Forest ensemble)
- **MLLO type:** `NonParametricModel`
- **Why selected:** Clearance rate is a key pharmacokinetic property. First regression task in the drug discovery set — adds output type diversity.
- **Encoding gap:** RFStacker is a stacked ensemble — MLLO has no EnsembleModel subtype. SMILES InputType gap applies.

---

### 6. TDC.PPBR_AZ
- **Source:** Therapeutics Data Commons — https://tdcommons.ai/
- **Domain:** Drug Discovery
- **Task:** Regression — what percentage of a drug binds to plasma proteins?
- **Input type:** SMILES string / molecular graph + RDKit descriptors
- **Output type:** Continuous value (binding percentage)
- **Dataset size:** 1,614 molecules
- **Best model:** Chemprop-RDKit
- **MLLO type:** `PolynomialModel`
- **Why selected:** Plasma protein binding affects drug availability — clinically essential. Chemprop-RDKit is a message-passing network with linear regression-style output layer.
- **Encoding gap:** Chemprop is architecturally a neural network — assigned to PolynomialModel per project mapping. SMILES InputType gap applies.

---

### 7. TDC.VDss_Lombardo
- **Source:** Therapeutics Data Commons — https://tdcommons.ai/
- **Domain:** Drug Discovery
- **Task:** Regression — what is the steady-state volume of distribution of a drug?
- **Input type:** SMILES string / molecular graph + RDKit descriptors
- **Output type:** Continuous value (volume in L/kg)
- **Dataset size:** 1,130 molecules
- **Best model:** Chemprop-RDKit
- **MLLO type:** `PolynomialModel`
- **Why selected:** Volume of distribution is a fundamental pharmacokinetic parameter. Same model family as PPBR_AZ, different biological property.
- **Encoding gap:** Same as TDC.PPBR_AZ.

---

### 8. Breast Cancer Wisconsin (Diagnostic)
- **Source:** UCI ML Repository — https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic
- **Domain:** Healthcare
- **Task:** Binary classification — is a tumor malignant or benign?
- **Input type:** Tabular (30 numeric features from cell nuclei measurements)
- **Output type:** Binary label
- **Dataset size:** 569 samples
- **Best model:** SVM (RBF kernel)
- **MLLO type:** `NonParametricModel`
- **Why selected:** Classic, well-understood benchmark. Clean tabular data, no missing values. Strong SVM baseline makes for a clean NonParametricModel encoding.
- **Notes:** No encoding gaps — clean MLLO fit.

---

### 9. Heart Disease (Cleveland)
- **Source:** UCI ML Repository — https://archive.ics.uci.edu/dataset/45/heart+disease
- **Domain:** Healthcare
- **Task:** Binary classification — does a patient have heart disease?
- **Input type:** Tabular (13 clinical features)
- **Output type:** Binary label
- **Dataset size:** 303 samples
- **Best model:** Logistic Regression
- **MLLO type:** `PolynomialModel`
- **Why selected:** Logistic Regression is the canonical PolynomialModel example. Well-known dataset with reproducible baselines.
- **Notes:** No encoding gaps — clean MLLO fit.

---

### 10. Chronic Kidney Disease
- **Source:** UCI ML Repository — https://archive.ics.uci.edu/dataset/336/chronic+kidney+disease
- **Domain:** Healthcare
- **Task:** Binary classification — does a patient have chronic kidney disease?
- **Input type:** Tabular (24 features, mixed numeric and categorical)
- **Output type:** Binary label
- **Dataset size:** 400 samples
- **Best model:** Random Forest
- **MLLO type:** `NonParametricModel`
- **Why selected:** Adds a mixed-type feature dataset (numeric + categorical) that tests MLLO's InputType description. Real clinical relevance.
- **Encoding gap:** High missing value rate — preprocessing strategy affects results but is not capturable in MLLO metadata.

---

### 11. Wholesale Customers *(added for ClusteringModel coverage)*
- **Source:** UCI ML Repository — https://archive.ics.uci.edu/dataset/292/wholesale+customers
- **Domain:** General / Retail
- **Task:** Unsupervised clustering — discover customer segments by annual spending across product categories
- **Input type:** Tabular (6 continuous spend features)
- **Output type:** Cluster assignment (no ground truth)
- **Dataset size:** 440 samples
- **Best model:** K-Means (k=3, validated by silhouette score)
- **MLLO type:** `ClusteringModel`
- **Why selected:** Clean, small tabular dataset ideal for K-Means. Well-documented UCI source. Covers ClusteringModel — the 4th MLLO type.
- **Encoding gap:** No ground truth labels — MLLO has no intrinsic evaluation metric support (silhouette, elbow criterion not encodable).

---

### 12. MNIST — PCA Pipeline *(added for DimensionalityReductionModel coverage)*
- **Source:** OpenML — https://www.openml.org/d/554
- **Domain:** General / Computer Vision
- **Task:** Reduce 784-dimensional digit images to 2–50 dimensions for visualization and downstream classification
- **Input type:** Image (28×28 grayscale, flattened to 784 features)
- **Output type:** Low-dimensional embedding
- **Dataset size:** 70,000 samples
- **Best model:** PCA (for reconstruction) + t-SNE (for 2D visualization)
- **MLLO type:** `DimensionalityReductionModel`
- **Why selected:** Canonical dimensionality reduction benchmark. PCA and t-SNE are the textbook examples for this MLLO type. Covers the 5th MLLO type.
- **Encoding gap:** MLLO has no `LowDimensionalEmbedding` OutputType. Unsupervised evaluation (reconstruction error, explained variance) not capturable.

---

## Summary Table

| # | Dataset | Source | Domain | Task Type | Best Model | MLLO Type |
|---|---|---|---|---|---|---|
| 1 | PathMNIST | MedMNIST | Medical Imaging | MultiClass Classification | ResNet-50 | ArtificialNeuralNetwork |
| 2 | ChestMNIST | MedMNIST | Medical Imaging | MultiLabel Classification | ResNet-18 | ArtificialNeuralNetwork |
| 3 | TDC.BBB_Martins | TDC | Drug Discovery | Binary Classification | MiniMol | ArtificialNeuralNetwork |
| 4 | TDC.DILI | TDC | Drug Discovery | Binary Classification | MapLight+GNN | NonParametricModel |
| 5 | TDC.Clearance_Hepatocyte_AZ | TDC | Drug Discovery | Regression | RFStacker | NonParametricModel |
| 6 | TDC.PPBR_AZ | TDC | Drug Discovery | Regression | Chemprop-RDKit | PolynomialModel |
| 7 | TDC.VDss_Lombardo | TDC | Drug Discovery | Regression | Chemprop-RDKit | PolynomialModel |
| 8 | Breast Cancer Wisconsin | UCI | Healthcare | Binary Classification | SVM | NonParametricModel |
| 9 | Heart Disease | UCI | Healthcare | Binary Classification | Logistic Regression | PolynomialModel |
| 10 | Chronic Kidney Disease | UCI | Healthcare | Binary Classification | Random Forest | NonParametricModel |
| 11 | Wholesale Customers | UCI | General | Clustering | K-Means | ClusteringModel |
| 12 | MNIST (PCA) | OpenML | General | Dimensionality Reduction | PCA + t-SNE | DimensionalityReductionModel |
