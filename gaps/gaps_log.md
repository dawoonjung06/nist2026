# MLLO Encoding Gaps Log

**Date:** 2026-06-25  
**Scope:** 12 datasets across 5 MLLO model types  
**Status:** Active — gaps to be addressed in future ontology revisions

---

## Summary

| Gap ID | Category | Affected Datasets | Severity |
|---|---|---|---|
| GAP-01 | OutputType missing variant | ChestMNIST (#2) | High |
| GAP-02 | InputType missing variant | TDC datasets (#3–7) | High |
| GAP-03 | ModelType missing subtype | TDC.Clearance_Hepatocyte_AZ (#5) | Medium |
| GAP-04 | Image InputType for non-ANN task | MNIST PCA (#12) | Low |
| GAP-05 | Unsupervised evaluation not capturable | Wholesale Customers (#11), MNIST PCA (#12) | Medium |
| GAP-06 | Data quality metadata absent | Chronic Kidney Disease (#10) | Low |

---

## GAP-01 — MultiLabelClassification OutputType missing

**Affected dataset:** ChestMNIST (#2)  
**Description:** ChestMNIST is a multi-label classification task — each X-ray image can simultaneously have multiple disease labels (e.g. atelectasis + effusion). MLLO's current OutputType vocabulary does not include a `MultiLabelClassification` variant. The dataset was encoded as `MultiClassClassification` as a workaround, which incorrectly implies mutually exclusive classes.  
**Proposed fix:** Add `MultiLabelClassification` to MLLO OutputType enumeration.  
**Impact:** Any dataset where multiple labels can co-occur (common in medical imaging, NLP tagging) cannot be accurately encoded.

---

## GAP-02 — MolecularGraph / SMILES InputType missing

**Affected datasets:** TDC.BBB_Martins (#3), TDC.DILI (#4), TDC.Clearance_Hepatocyte_AZ (#5), TDC.PPBR_AZ (#6), TDC.VDss_Lombardo (#7)  
**Description:** All TDC drug discovery datasets use molecular SMILES strings or molecular graphs as input — not tabular feature vectors. MLLO's InputType has no variant for molecular data. All 5 datasets were encoded as `TabularData` as a workaround, losing the graph-structured input modality entirely.  
**Proposed fix:** Add `MolecularGraph` (and optionally `SMILESString`) to MLLO InputType enumeration.  
**Impact:** The entire drug discovery domain cannot be accurately represented. This is a significant gap for any biomedical MLLO application.

---

## GAP-03 — EnsembleModel not a first-class MLLO type

**Affected dataset:** TDC.Clearance_Hepatocyte_AZ (#5)  
**Description:** The best model for this dataset is RFStacker — a stacked ensemble combining multiple Random Forest models with a meta-learner. MLLO has no `EnsembleModel` type or subtype. The model was encoded as `NonParametricModel / EnsembleModel` (subtype), but this subtype is not in the official MLLO vocabulary.  
**Proposed fix:** Add `EnsembleModel` either as a standalone MLLO type or as a valid subtype under `NonParametricModel`.  
**Impact:** Stacking, bagging, and boosting architectures (common in tabular ML) cannot be precisely described.

---

## GAP-04 — DimensionalityReductionModel OutputType missing

**Affected dataset:** MNIST PCA (#12)  
**Description:** The output of a dimensionality reduction model is a low-dimensional embedding — not a label, not a continuous value, and not a cluster assignment. MLLO has no `LowDimensionalEmbedding` OutputType.  
**Proposed fix:** Add `LowDimensionalEmbedding` to MLLO OutputType, or create a separate `EmbeddingOutput` variant.  
**Impact:** PCA, t-SNE, UMAP, and autoencoder outputs cannot be typed correctly.

---

## GAP-05 — Unsupervised evaluation metrics not capturable

**Affected datasets:** Wholesale Customers (#11), MNIST PCA (#12)  
**Description:** Both `ClusteringModel` and `DimensionalityReductionModel` tasks are unsupervised — there are no ground truth labels. Standard supervised evaluation metrics (accuracy, F1, RMSE) do not apply. MLLO currently has no mechanism to encode intrinsic evaluation metrics such as silhouette score, Davies-Bouldin index, or reconstruction error.  
**Proposed fix:** Add an `UnsupervisedEvaluationMetric` metadata class to MLLO, with instances for silhouette, elbow criterion, reconstruction error, and explained variance ratio.  
**Impact:** Unsupervised models cannot have their evaluation strategy described in MLLO metadata.

---

## GAP-06 — Data quality / preprocessing metadata absent

**Affected dataset:** Chronic Kidney Disease (#10)  
**Description:** The Chronic Kidney Disease dataset has a significant rate of missing values across its 24 features. The preprocessing strategy (imputation method, dropped features) materially affects model performance and reproducibility. MLLO has no metadata fields for data quality indicators or preprocessing pipeline description.  
**Proposed fix:** Add optional `DataQuality` metadata fields: `missing_value_rate`, `imputation_strategy`, `preprocessing_steps`.  
**Impact:** Reproducibility of results is reduced for any dataset with data quality issues.

---

## Notes for Future Work

- GAP-02 (molecular inputs) is the highest-priority gap for the drug discovery use case. Resolving it unblocks accurate encoding of 5 of the 12 datasets.
- GAP-01 (multi-label) is the highest-priority gap for the medical imaging use case.
- AssociationRuleModel was excluded from this iteration. Future work should identify a suitable transaction-format dataset (e.g. market basket, EHR diagnosis co-occurrence) to cover this type.
