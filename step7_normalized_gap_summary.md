# Step 7 — Normalized Gap Summary

Source logs: BreastMNIST/ResNet18 gap log (11 items) + PathMNIST/CustomNet gap log (8 items).
This step merges duplicates, groups by theme, and ranks by recurrence — how many of the two
encoding exercises independently hit the same missing class/property. Recurring gaps are
stronger evidence of a real ontology gap (not a one-off quirk of a single notebook) and are
prioritized for Step 8.

## Gap Themes, Ranked by Recurrence

### Tier 1 — Hit in both encodings (strongest signal)

| # | Gap | Seen in | Impact |
|---|---|---|---|
| 1 | No evaluation-metric classes beyond `ClassificationAccuracy` — no Precision, Recall, F1, Support, AUC, or ROC | BreastMNIST + PathMNIST | High — every classification report and every AUC score from both notebooks has nowhere principled to live. This is the single biggest recurring gap. |
| 2 | No `PyTorch` class under `MachineLearningFramework` (only Tensorflow, Keras exist) | BreastMNIST + PathMNIST | High — both notebooks are PyTorch-based; framework provenance can't be recorded at all. |
| 3 | No `CrossEntropyLoss` subclass of `LossFunction` | BreastMNIST + PathMNIST | Medium — falls back to generic `LossFunction`, losing which specific loss was used. |
| 4 | No dedicated hyperparameter subclasses for learning rate, momentum, or weight decay (only generic `Hyperparameter`) | BreastMNIST + PathMNIST | Medium — `BatchSize` and `EpochNumber` exist as named subclasses, but the other common hyperparameters don't, which is an inconsistent level of granularity within the same ontology section. |
| 5 | No dedicated subtype for data-loading/batching operations (`DataLoader` equivalents fall back to generic `DataProcessingOperation`) | BreastMNIST + PathMNIST | Medium — same generic-fallback pattern as #3 and #4. |
| 6 | Optimizer taxonomy is thin — only `AdamOptimizer` is a named subclass; SGD has none, and even `AdamOptimizer` can't distinguish the decoupled-weight-decay (AdamW) variant | BreastMNIST + PathMNIST | Medium — optimizer choice is a first-class experimental variable and currently under-modeled. |

### Tier 2 — Hit once, but likely to recur once more model types are encoded

| # | Gap | Seen in | Impact |
|---|---|---|---|
| 7 | No "architecture modification" / transfer-learning operation class — `GainOfRole`/`LossOfRole` is a usable but stretched fit for swapping a model's final layer | BreastMNIST | Medium — likely to reappear with any other fine-tuning example. |
| 8 | No batch-normalization class (`BatchNorm2d` has no home) | PathMNIST | Low-medium — architecture-detail gap, will recur with any CNN example that uses batch norm. |
| 9 | No way to distinguish a custom-trained architecture from a pretrained one (both map to the same generic `ConvolutionalNeuralNetwork`/`ArtificialNeuralNetwork` class) | BreastMNIST + PathMNIST (same underlying issue, different angle) | Medium — provenance of model weights is lost. |
| 10 | No dedicated subtype for data-acquisition/download operations (falls back to generic `DataProcessingOperation`, and has no clean `hasDataInput` since the source is external) | BreastMNIST + PathMNIST | Low — minor modeling awkwardness rather than a hard blocker. |

### Tier 3 — One-off / domain-specific

| # | Gap | Seen in | Impact |
|---|---|---|---|
| 11 | No medical-imaging-modality property (e.g. recording that BreastMNIST is ultrasound-derived) | BreastMNIST only | Low — domain-specific, won't recur once we move to non-medical datasets (Wine, Iris, Mall Customers, etc.) |

## Resolved Since Initial Logging (no longer gaps — confirmed real classes exist)

For completeness — these were flagged as gaps before the actual `mllo.rdf` file was checked
directly, and turned out to be real, defined classes:
- Train/val/test split operation → `MachineLearningDataSetPartitioning` exists
- Image normalization/scaling operation → `FeatureScalingOperation` exists
- CNN/ResNet architecture class → `ConvolutionalNeuralNetwork` exists
- Dataset-vs-generic-DataItem distinction → `RawDataSet`, `TrainingDataSet`, `ValidationDataSet`,
  `TestDataSet`, `PreProcessedDataSet` all exist

This is worth keeping in the record as a caution for Step 8: always verify against the live file
before proposing a new class — some "gaps" are actually just undiscovered existing classes.

## Summary Table for Step 8 Input

| Priority | Gap | Recommended action type |
|---|---|---|
| 1 | Missing evaluation metrics (Precision/Recall/F1/AUC/ROC) | Add new classes |
| 2 | Missing `PyTorch` framework class | Add new class |
| 3 | Missing `CrossEntropyLoss` subclass | Add new class |
| 4 | Missing LearningRate/Momentum/WeightDecay hyperparameter subclasses | Add new classes (match existing `BatchSize`/`EpochNumber` pattern) |
| 5 | Missing batching/DataLoader operation subtype | Add new class |
| 6 | Thin optimizer taxonomy (no SGD, no AdamW distinction) | Add new classes |
| 7 | No transfer-learning/architecture-modification operation class | Add new class or clarify `GainOfRole`/`LossOfRole` usage guidance |
| 8 | No BatchNorm class | Add new class |
| 9 | No custom-vs-pretrained model provenance property | Add new data/object property |
| 10 | No data-acquisition operation subtype | Add new class |
