# MLLO Model Type Definitions

This document defines the 6 MLLO model types used in this project, with examples and notes on how they map to real-world ML models.

---

## 1. ArtificialNeuralNetwork

**Definition:** Models that learn hierarchical representations through multiple layers of connected nodes, using gradient-based optimization.

**Includes:** CNNs, MLPs, ResNets, Transformers, LSTMs, Message-Passing Neural Networks  
**Typical tasks:** Image classification, sequence modeling, graph property prediction  
**Datasets in this project:** PathMNIST, ChestMNIST, TDC.BBB_Martins

---

## 2. NonParametricModel

**Definition:** Models that do not assume a fixed parametric form for the data distribution. The model complexity can grow with the data.

**Includes:** Decision Trees, Random Forest, SVM, KNN, Gradient Boosted Trees  
**Typical tasks:** Classification, regression on tabular data  
**Datasets in this project:** TDC.DILI, TDC.Clearance_Hepatocyte_AZ, Breast Cancer Wisconsin, Chronic Kidney Disease

---

## 3. PolynomialModel

**Definition:** Models that represent the relationship between inputs and outputs as a polynomial (or generalized linear) function.

**Includes:** Linear Regression, Logistic Regression, Ridge, Lasso, Polynomial Regression  
**Typical tasks:** Binary classification, regression  
**Datasets in this project:** TDC.PPBR_AZ, TDC.VDss_Lombardo, Heart Disease

---

## 4. ClusteringModel

**Definition:** Unsupervised models that partition data points into groups (clusters) based on similarity, without ground truth labels.

**Includes:** K-Means, DBSCAN, Hierarchical Clustering, GMM  
**Typical tasks:** Customer segmentation, anomaly detection, exploratory analysis  
**Datasets in this project:** Wholesale Customers

---

## 5. DimensionalityReductionModel

**Definition:** Models that transform high-dimensional data into a lower-dimensional representation, preserving meaningful structure.

**Includes:** PCA, t-SNE, UMAP, Autoencoders, ICA  
**Typical tasks:** Visualization, feature extraction, preprocessing for downstream models  
**Datasets in this project:** MNIST (PCA)

---

## 6. AssociationRuleModel *(excluded from this iteration)*

**Definition:** Models that discover co-occurrence patterns and association rules between items in transaction datasets.

**Includes:** Apriori, FP-Growth, Eclat  
**Typical tasks:** Market basket analysis, EHR diagnosis pattern mining  
**Datasets in this project:** None — excluded due to no suitable transaction-format dataset in the current scope. Planned for future iteration.

---

## Type Selection Rationale

5 of 6 types were targeted. `AssociationRuleModel` was excluded because:

1. All selected domains (medical imaging, drug discovery, healthcare) use instance-level prediction tasks, not transaction mining.
2. No suitable publicly available dataset in these domains fits the transaction-format input required by Apriori/FP-Growth.
3. Adding a forced dataset outside the established domains would reduce cohesion of the demo.
