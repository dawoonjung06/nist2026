# MLLO Demo — Dataset & Model Repository Review

This repository documents the dataset candidates, MLLO model type assignments, encoded metadata, and gap analysis for the MLLO (Machine Learning Lifecycle Ontology) demonstration project.

## What is MLLO?

MLLO is an ontology for describing machine learning models and their lifecycle. It defines a controlled vocabulary of model types, input/output modalities, and metadata properties that can be applied to real-world datasets and models.

## Targeted MLLO Model Types (5 of 6)

| MLLO Type | Examples | Status |
|---|---|---|
| `ArtificialNeuralNetwork` | CNNs, MLPs, ResNets | ✅ Covered (3 datasets) |
| `NonParametricModel` | Decision Trees, SVM, Random Forest, KNN | ✅ Covered (4 datasets) |
| `PolynomialModel` | Linear Regression, Logistic Regression | ✅ Covered (3 datasets) |
| `ClusteringModel` | K-Means, DBSCAN | ✅ Covered (1 dataset) |
| `DimensionalityReductionModel` | PCA, t-SNE | ✅ Covered (1 dataset) |
| `AssociationRuleModel` | Apriori, FP-Growth | ❌ Excluded — no natural fit in medical/drug discovery domains |

## Repository Structure

```
mllo-demo/
├── README.md                        ← this file
├── metadata/
│   ├── datasets.csv                 ← all 12 dataset candidates with MLLO fields
│   ├── mllo_encoded.json            ← full MLLO metadata encoding per dataset
│   └── model_type_coverage.json     ← summary of type → dataset mappings
├── gaps/
│   └── gaps_log.md                  ← documented MLLO encoding gaps
└── docs/
    └── mllo_type_definitions.md     ← definitions of the 6 MLLO types
```

## Dataset Sources

| Source | Domain | Datasets Used |
|---|---|---|
| [MedMNIST](https://medmnist.com/) | Medical imaging | PathMNIST, ChestMNIST |
| [TDC (Therapeutics Data Commons)](https://tdcommons.ai/) | Drug discovery | BBB_Martins, DILI, Clearance_Hepatocyte_AZ, PPBR_AZ, VDss_Lombardo |
| [UCI ML Repository](https://archive.ics.uci.edu/) | Healthcare / general | Breast Cancer Wisconsin, Heart Disease, Chronic Kidney Disease, Wholesale Customers, MNIST (PCA) |

## Quick Summary

- 12 datasets across 3 domains (medical imaging, drug discovery, healthcare/general)
- 5 MLLO model types instantiated
- 6 encoding gaps identified (see `gaps/gaps_log.md`)
- Work-in-progress: future months will cover `AssociationRuleModel` and expand to additional domains

## Timeline

| Period | Work |
|---|---|
| This week | Repository review, candidate selection, MLLO metadata encoding, gap analysis |
| Next month+ | Extend to remaining MLLO type, add evaluation metrics, integrate with full MLLO ontology |
