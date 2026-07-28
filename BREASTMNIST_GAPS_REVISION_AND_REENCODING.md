# BreastMNIST: Gaps Summary, MLLO Revision Proposal, and Re-encoding Comparison

> **Source notebook:** `medmnist-breastmnist-resnet18.ipynb`  
> **Source ontology:** Machine Learning Lifecycle Ontology (MLLO)  
> **Original encoded artifact:** [`../ontology/BreastMNIST_Encoding.rdf`](../ontology/BreastMNIST_Encoding.rdf)  
> **Revised ontology draft:** [`../ontology/MLLO_Revision_Draft.rdf`](../ontology/MLLO_Revision_Draft.rdf)  
> **Re-encoded artifact:** [`../ontology/BreastMNIST_Reencoded_RevisedMLLO.rdf`](../ontology/BreastMNIST_Reencoded_RevisedMLLO.rdf)

---

## 1. BreastMNIST Workflow Summary

The BreastMNIST notebook trains a pretrained ResNet18 model for binary image classification.

**Dataset and pipeline details**

- Training set: 546 images
- Validation set: 78 images
- Test set: 156 images
- Original image size: `224 × 224`
- Labels: binary classes `0` and `1`
- Model: pretrained ResNet18
- Final fully connected layer: replaced with 2 output units
- Optimizer: `AdamW`
- Learning rate: `0.0001`
- Weight decay: `0.0001`
- Loss function: `CrossEntropyLoss`
- Batch size: `32`
- Total epochs: `11`
- Test accuracy: `0.9103`

**Training transform pipeline**

```text
Grayscale(num_output_channels=3)
→ RandomHorizontalFlip()
→ RandomRotation(10)
→ ToTensor()
→ Normalize(mean=[0.5, 0.5, 0.5], std=[0.5, 0.5, 0.5])
```

**Validation and test transform pipeline**

```text
Grayscale(num_output_channels=3)
→ ToTensor()
→ Normalize(mean=[0.5, 0.5, 0.5], std=[0.5, 0.5, 0.5])
```

---

## 2. Normalized MLLO Gaps

The original MLLO could represent the broad machine learning workflow, but several important details had to be stored using generic classes or comments.

| # | Gap | Why it is a gap | Original fallback | Priority |
|---|---|---|---|---|
| 1 | No dedicated AdamW optimizer class | The notebook uses AdamW, but the original ontology cannot distinguish it from other optimization algorithms. | Generic `OptimizationAlgorithm` | High |
| 2 | Missing learning rate and weight decay classes | These are essential optimizer settings needed to reproduce training. | Stored only in comments | High |
| 3 | No named CrossEntropyLoss subclass | The loss function can only be represented generically. | Generic `LossFunction` | High |
| 4 | No PyTorch framework class | The complete implementation is written in PyTorch, but the framework cannot be represented directly. | Not encoded or stored in comments | High |
| 5 | No pretrained-model provenance pattern | The model uses pretrained ResNet18 DEFAULT weights, but MLLO cannot clearly distinguish pretrained models from models trained from scratch. | Stored only in comments | High |
| 6 | Limited evaluation metric support | Accuracy can be represented, but precision, recall, F1-score, and support cannot be encoded as class-specific results. | Stored in evaluation comments | High |
| 7 | No dedicated validation dataset representation | The validation split does not have a clear dedicated class in the original ontology. | Generic or fallback dataset class | Medium |
| 8 | No data-loading or batching operation subtype | NumPy loading and PyTorch DataLoader behavior are part of the workflow but must use a generic processing class or comments. | Generic `DataProcessingOperation` | Medium |
| 9 | Transform order is not represented | `isComposedOf` records membership but not the order of preprocessing operations. | Operation order stored in comments | Medium |
| 10 | Transform parameters are weakly represented | Rotation angle, channel count, normalization mean, and standard deviation are not modeled with dedicated parameters. | Stored in comments | Medium |
| 11 | Per-epoch training history is not represented | The notebook performs 11 epochs, but per-epoch loss and validation accuracy are not structured in RDF. | Only total epoch count encoded | Medium |
| 12 | Dataset shape and label semantics are incomplete | Image dimensions, sample counts, label array shape, and binary label meanings do not have a consistent representation. | Stored in comments | Low/Medium |

---

## 3. Evidence Behind the Main Gaps

### 3.1 Optimizer and hyperparameters

The notebook uses:

```text
AdamW(lr=0.0001, weight_decay=0.0001)
```

The original MLLO can represent a generic optimization algorithm, but it cannot identify AdamW or explicitly store learning rate and weight decay as dedicated hyperparameter types. This reduces reproducibility and prevents direct queries such as “Which models used AdamW with weight decay?”

### 3.2 Loss-function specificity

The workflow uses `CrossEntropyLoss`, but the original MLLO only provides a general `LossFunction` class. The encoding therefore loses the exact loss-function identity unless it is stored in a comment.

### 3.3 Transfer learning and model provenance

The model is a pretrained ResNet18 using default pretrained weights, with the final classification layer replaced by a two-output layer. The original ontology can represent a convolutional neural network and the final fully connected layer, but it cannot express that the model was initialized from pretrained weights.

### 3.4 Evaluation metrics

The notebook reports:

| Class | Precision | Recall | F1-score | Support |
|---|---:|---:|---:|---:|
| 0 | 0.85 | 0.81 | 0.83 | 42 |
| 1 | 0.93 | 0.95 | 0.94 | 114 |

The original MLLO supports classification accuracy, but it does not provide a clear way to represent a metric value scoped to a specific class label. Storing all of these values in one comment makes them readable but not queryable.

### 3.5 Preprocessing reproducibility

The training pipeline includes grayscale-to-RGB conversion, random horizontal flipping, random rotation, tensor conversion, and normalization. MLLO can represent some operations broadly, but it does not capture the exact execution order or all operation parameters.

---

## 4. MLLO Revision Proposal

The following additions were proposed to address the highest-priority BreastMNIST gaps.

### 4.1 Proposed new classes

#### Optimizer, loss, and hyperparameters

- `AdamWOptimizationAlgorithm`
- `CrossEntropyLoss`
- `LearningRate`
- `WeightDecay`

#### Framework and execution environment

- `PyTorch`

#### Data handling

- `ValidationDataSet`
- `DataLoadingOperation`
- `DataBatchingOperation`

#### Model provenance

- `PretrainedModel`
- `PretrainedModelParameterArtifact`

#### Evaluation metrics

- `MetricResult`
- `Precision`
- `Recall`
- `F1Score`
- `SupportCount`
- `ClassLabel`

#### Preprocessing and training history

- `DataPreparationStep`
- `TrainingEpoch`
- `TrainingLoss`
- `ValidationAccuracy`

---

### 4.2 Proposed new object properties

| Property | Domain → Range | Purpose |
|---|---|---|
| `usesFramework` | Training → Framework | Connects the training activity to PyTorch. |
| `usesLossFunction` | Training → LossFunction | Explicitly links training to CrossEntropyLoss. |
| `hasMetricResult` | ModelEvaluation → MetricResult | Connects evaluation to individual measured results. |
| `usesMetric` | MetricResult → PerformanceMetric | Identifies whether the result is precision, recall, F1, or support. |
| `evaluatesClassLabel` | MetricResult → ClassLabel | Records the class to which a metric value applies. |
| `usesPretrainedParameters` | PretrainedModel → PretrainedModelParameterArtifact | Records the pretrained weights used to initialize a model. |
| `hasStep` | DataPreparationPipeline → DataPreparationStep | Supports explicit preprocessing steps. |
| `executesOperation` | DataPreparationStep → DataProcessingOperation | Connects an ordered step to its operation. |
| `hasEpoch` | MachineLearningTraining → TrainingEpoch | Connects training to individual epochs. |

---

### 4.3 Proposed new data properties

| Property | Suggested value type | Purpose |
|---|---|---|
| `hasMetricValue` | decimal | Stores precision, recall, F1, accuracy, or loss values. |
| `hasSupportCount` | integer | Stores the number of examples supporting a class metric. |
| `stepIndex` | integer | Stores preprocessing operation order. |
| `hasEpochIndex` | integer | Identifies an individual training epoch. |

---

### 4.4 Clarifications and constraints

The revision should also clarify or constrain several existing patterns:

1. **Clarify `executed`.** It should not be used as a general connection for models, optimizers, loss functions, and software without clear semantics.
2. **Separate configuration from measurement.** `hasConfigurationSettingValue` should remain for hyperparameters and settings, while metric results should use `hasMetricValue`.
3. **Separate metric type from metric result.** `F1Score` represents a type of metric, while `BreastF1_Class1` represents a measured result of `0.94` for class 1.
4. **Standardize dataset split representation.** Training, validation, and test datasets should follow one consistent pattern.
5. **Support ordered pipelines.** `isComposedOf` alone is not sufficient where preprocessing order changes model behavior.
6. **Constrain numeric values.** Learning rate, weight decay, accuracy, precision, recall, and F1 should use decimal literals; support and epoch indexes should use integer literals.

---

## 5. Re-encoding Against the Revised MLLO

The BreastMNIST metadata was re-encoded after applying the proposed ontology additions.

### 5.1 Re-encoding comparison

| Metadata item | Original MLLO encoding | Revised MLLO encoding | Improvement |
|---|---|---|---|
| Data loading | Generic `DataProcessingOperation` | `DataLoadingOperation` | Makes loading activities directly queryable. |
| Validation split | Generic/fallback dataset type | `ValidationDataSet` | Clearly distinguishes validation data from training and test data. |
| AdamW optimizer | Generic `OptimizationAlgorithm` | `AdamWOptimizationAlgorithm` | Preserves exact optimizer identity. |
| CrossEntropyLoss | Generic `LossFunction` | `CrossEntropyLoss` | Preserves exact loss-function identity. |
| Learning rate | Comment only | `BreastLearningRate_0_0001` | Makes the value structured and queryable. |
| Weight decay | Comment only | `BreastWeightDecay_0_0001` | Makes regularization settings explicit. |
| PyTorch | Not encoded | `BreastPyTorch_Framework` typed as `PyTorch` | Records the implementation framework. |
| Pretrained model | Comment only | `PretrainedModel` | Distinguishes transfer learning from training from scratch. |
| Pretrained weights | Comment only | `BreastResNet18_DefaultWeights` | Captures the model initialization artifact. |
| DataLoader batching | Comment only | `DataBatchingOperation` | Represents batching as part of the lifecycle. |
| Precision | Evaluation comment | Class-scoped `MetricResult` individuals | Allows precision to be queried by class. |
| Recall | Evaluation comment | Class-scoped `MetricResult` individuals | Allows recall to be queried by class. |
| F1-score | Evaluation comment | Class-scoped `MetricResult` individuals | Allows F1-score to be queried by class. |
| Support | Evaluation comment | Class-scoped `MetricResult` individuals | Preserves class sample counts. |
| Transform order | Comment or unordered composition | Ordered `DataPreparationStep` pattern | Improves reproducibility. |
| Training history | Total epoch count only | Proposed `TrainingEpoch` individuals | Supports per-epoch loss and validation accuracy. |

---

### 5.2 Important revised individuals

The revised encoding adds or specializes individuals such as:

```text
BreastAdamW_Optimizer
BreastCrossEntropyLoss
BreastLearningRate_0_0001
BreastWeightDecay_0_0001
BreastPyTorch_Framework
BreastResNet18_DefaultWeights
BreastTrainBatchingOperation
BreastEvalBatchingOperation
BreastClassLabel_0
BreastClassLabel_1
BreastPrecision_Class0
BreastRecall_Class0
BreastF1_Class0
BreastSupport_Class0
BreastPrecision_Class1
BreastRecall_Class1
BreastF1_Class1
BreastSupport_Class1
```

The revised training activity can now explicitly include:

```text
usesFramework → BreastPyTorch_Framework
usesLossFunction → BreastCrossEntropyLoss
hasConfigurationVariable → BreastBatchSize_32
hasConfigurationVariable → BreastEpochNumber_11
hasConfigurationVariable → BreastLearningRate_0_0001
hasConfigurationVariable → BreastWeightDecay_0_0001
```

The revised evaluation activity can now explicitly connect to class-level metric results rather than storing them in one comment.

---

## 6. Overall Result

The revised BreastMNIST encoding captures substantially more of the original notebook as structured RDF.

The main improvement is not simply that more terms were added. The important change is that previously hidden details are now directly queryable, including:

- the exact optimizer and loss function
- learning rate and weight decay
- the PyTorch framework
- pretrained model initialization
- validation data
- batching operations
- class-specific precision, recall, F1-score, and support
- preprocessing order

This makes the encoding more useful for reproducibility, comparison, competency questions, and future automated reasoning.

---

## 7. Remaining Limitations

Even after the revision, several issues remain:

- The semantic meaning of BreastMNIST class labels `0` and `1` should be linked to authoritative dataset documentation.
- Hardware, runtime environment, random seeds, and software package versions are not fully represented.
- The full internal ResNet18 architecture is not expanded layer by layer.
- Per-epoch training and validation results require additional individuals if complete training history is needed.
- Ordered pipeline modeling adds complexity and may require stronger cardinality constraints.
- Some operation parameters still rely on comments unless a general parameter-value pattern is introduced.

---

## 8. Repository Artifacts

| Artifact | Purpose |
|---|---|
| [`METADATA_ENCODING_AND_GAP_REPORT.md`](METADATA_ENCODING_AND_GAP_REPORT.md) | Original metadata encoding and detailed gap log |
| [`BREASTMNIST_GAPS_REVISION_AND_REENCODING.md`](BREASTMNIST_GAPS_REVISION_AND_REENCODING.md) | Combined gaps summary, ontology revision proposal, and re-encoding comparison |
| [`../ontology/BreastMNIST_Encoding.rdf`](../ontology/BreastMNIST_Encoding.rdf) | Original encoding against the existing MLLO |
| [`../ontology/MLLO_Revision_Draft.rdf`](../ontology/MLLO_Revision_Draft.rdf) | Proposed updated ontology draft |
| [`../ontology/BreastMNIST_Reencoded_RevisedMLLO.rdf`](../ontology/BreastMNIST_Reencoded_RevisedMLLO.rdf) | Updated metadata encoded against the revised MLLO |

