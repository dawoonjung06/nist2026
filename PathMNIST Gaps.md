# PathMNIST: Metadata Encoding and Gap Report

> **Source ontology:** [`mllo.rdf`](./mllo.rdf) (Machine Learning Lifecycle Ontology), imports IOF Core and BFO
> **Encoded artifact:** [`PathMNIST.rdf`](./PathMNIST.rdf), 30 individuals, verified against ontology source

---

**Pipeline-level parameters:** `NUM_EPOCHS=3`, `BATCH_SIZE=128` (train) / `256` (eval), optimizer `SGD(lr=0.001, momentum=0.9)`, loss `CrossEntropyLoss`, transform `ToTensor() → Normalize(mean=[.5], std=[.5])`.

## Encoding Table

| # | Metadata Item | MLLO Class | Individual | Status |
|---|---|---|---|---|
| 1 | PathMNIST raw download | `iof-constr:RawDataSet` | `PathMNIST_RawData` | ✅ Confirmed |
| 2 | Download operation | `iof-constr:DataProcessingOperation` | `DownloadPathMNISTOperation` | ✅ Confirmed (generic) |
| 3 | Train split | `iof-constr:TrainingDataSet` | `PathMNIST_TrainDataset` | ✅ Confirmed |
| 4 | Test split | `iof-constr:TestDataSet` | `PathMNIST_TestDataset` | ✅ Confirmed |
| 5 | `ToTensor()` | `iof-constr:TypeCastingOperation` | `ToTensorOp_PathMNIST` | ✅ Confirmed |
| 6 | `Normalize(...)` | `iof-constr:FeatureScalingOperation` | `NormalizeOp_PathMNIST` | ✅ Confirmed |
| 7 | Transform pipeline | `iof-constr:MachineLearningDataPreparationPipeline` | `PathMNIST_TransformPipeline` | ✅ Confirmed |
| 8 | Transformed train set | `iof-constr:PreProcessedDataSet` | `PathMNIST_TrainDataset_Transformed` | ✅ Confirmed |
| 9 | Conv2d ×5 | `iof-constr:ConvolutionalLayer` | `ConvLayer_1` … `ConvLayer_5` | ✅ Confirmed |
| 10 | MaxPool2d ×2 | `iof-constr:PoolingLayer` | `PoolLayer_1`, `PoolLayer_2` | ✅ Confirmed |
| 11 | Linear ×3 | `iof-constr:FullyConnectedLayer` | `FCLayer_1` … `FCLayer_3` | ✅ Confirmed |
| 12 | `Net` model | `iof-constr:ConvolutionalNeuralNetwork` | `PathMNIST_CustomNet` | ✅ Confirmed |
| 13 | `BATCH_SIZE=128` | `iof-constr:BatchSize` | `BatchSize_128` | ✅ Confirmed |
| 14 | `NUM_EPOCHS=3` | `iof-constr:EpochNumber` | `EpochNumber_3` | ✅ Confirmed |
| 15 | Each epoch | `iof-constr:Epoch` | `Epoch_1`, `Epoch_2`, `Epoch_3` | ✅ Confirmed |
| 16 | SGD optimizer | `iof-constr:OptimizationAlgorithm` | `SGD_Optimizer` | ⚠️ Generic fallback (gap) |
| 17 | CrossEntropyLoss | `iof-constr:LossFunction` | `CrossEntropyLoss_Instance` | ⚠️ Generic fallback (gap) |
| 18 | Training loop | `iof-constr:MachineLearningTraining` | `PathMNIST_Training` | ✅ Confirmed |
| 19 | Train-set evaluation | `iof-constr:ModelEvaluation` | `PathMNIST_TrainEvaluation` | ✅ Confirmed |
| 20 | Test-set evaluation | `iof-constr:ModelEvaluation` | `PathMNIST_TestEvaluation` | ✅ Confirmed |
| 21 | Train accuracy 0.864 | `iof-constr:ClassificationAccuracy` | `TrainAccuracy_0.864` | ✅ Confirmed |
| 22 | Test accuracy 0.758 | `iof-constr:ClassificationAccuracy` | `TestAccuracy_0.758` | ✅ Confirmed |
| 23 | AUC 0.988 / 0.943 | *No class exists* | Not encoded | ❌ Gap |
| 24 | BatchNorm2d (×5) | *No class exists* | Not encoded | ❌ Gap |

**Object properties used** (confirmed in `mllo.rdf`): `hasDataInput`, `hasDataOutput`, `isComposedOf`, `executed`, `hasConfigurationVariable`
**Data properties used:** `hasConfigurationSettingValue` (integer and decimal literals)

## Confirmed Ontology Gaps

Each gap was confirmed by direct inspection of `mllo.rdf` — searching the class hierarchy under the relevant superclass and finding no matching subclass.

### 5.1 No Batch Normalization Class
No class in MLLO represents batch normalization. This model applies `nn.BatchNorm2d` after every one of its 5 convolutional layers — the most frequently recurring unencodable element in this artifact.

### 5.2 No Evaluation Metric Classes Beyond Accuracy
Only `iof-constr:ClassificationAccuracy` exists under `PerformanceMetric`. Precision, Recall, F1, Support, and AUC/ROC have no representation. This model's AUC scores (0.988 train, 0.943 test) can't be encoded under any existing class.

### 5.3 Thin Optimizer Taxonomy
Only `iof-constr:AdamOptimizer` exists under `OptimizationAlgorithm`. SGD, used here, has no dedicated class.

### 5.4 No Named Loss Function Subclasses
`iof-constr:LossFunction` has no subclasses; `CrossEntropyLoss` falls back to the generic class.

### 5.5 Incomplete Hyperparameter Taxonomy
`BatchSize` and `EpochNumber` are named subclasses of `Hyperparameter`, but `LearningRate` and `Momentum` (both explicitly set here: `lr=0.001`, `momentum=0.9`) are not.

### 5.6 No Architecture Provenance Distinction
This hand-built `Net` and the pretrained ResNet18 from the BreastMNIST encoding both instantiate the same `ConvolutionalNeuralNetwork` class — no property records pretrained vs. from-scratch.

### 5.7 No Data-Loading/Batching Operation Subtype
The download operation and any DataLoader-equivalent fall back to generic `DataProcessingOperation`.

### 5.8 No PyTorch Framework Class
Only `Tensorflow` and `Keras` exist under `MachineLearningFramework`. Both encodings in this project (BreastMNIST, PathMNIST) are PyTorch-based.
