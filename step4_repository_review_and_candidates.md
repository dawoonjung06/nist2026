# Step 4 — Repository Review and Candidate Selection

## MLLO Model Types (verified in mllo.rdf)

mllo.rdf defines exactly 6 direct subclasses of `iof-constr:MachineLearningModel`:

1. ArtificialNeuralNetwork
2. AssociationRuleModel
3. ClusteringModel
4. DimensionalityReductionModel
5. NonParametricModel
6. PolynomialModel

Per the task instructions, 5 of these 6 are targeted. ArtificialNeuralNetwork is already covered
(BreastMNIST/ResNet18 and PathMNIST/custom CNN, both encoded in prior steps). This note selects
one concrete candidate for each of the remaining 4 types, plus one alternate (NonParametricModel)
to keep a spare in reserve — giving 5 targeted types total with real, working notebooks.

## Candidates

### 1. AssociationRuleModel
- **Task:** Market basket analysis using the Apriori algorithm
- **Dataset:** Groceries / Online Retail transaction data
- **Notebook:** https://www.kaggle.com/code/prasad22/market-basket-analysis-with-apriori-algorithm
- **Alternate:** https://www.kaggle.com/code/timothyabwao/market-basket-analysis-using-the-apriori-algorithm
- **Why it fits:** Apriori produces explicit association rules (antecedent -> consequent, with
  support/confidence/lift), which maps directly onto AssociationRuleModel rather than being a
  stretch-fit onto a generic class.

### 2. ClusteringModel
- **Task:** Customer segmentation using K-Means
- **Dataset:** Mall Customer Segmentation Data (Age, Annual Income, Spending Score)
- **Notebook:** https://www.kaggle.com/code/sohamohajeri/customer-segmentation-analysis-by-kmeans-cluster
- **Alternate:** https://www.kaggle.com/code/heeraldedhia/kmeans-clustering-for-customer-data
- **Why it fits:** Unsupervised K-Means directly instantiates ClusteringModel; the elbow-method
  step for choosing K is a useful extra hyperparameter-selection process to encode.

### 3. DimensionalityReductionModel
- **Task:** PCA on the UCI Wine dataset (13 chemical-analysis features -> reduced components)
- **Dataset:** UCI Wine (178 samples, 13 features, 3 cultivar classes) — https://archive.ics.uci.edu/dataset/109/wine
- **Notebook:** https://www.kaggle.com/code/murats/pca-and-lda-dimensional-reduction-on-wine-dataset
- **Alternate:** https://www.kaggle.com/sonalisingh1411/pca-on-wine-dataset
- **Why it fits:** PCA is a canonical DimensionalityReductionModel instance, and the Wine dataset
  is small enough to fully trace every component/eigenvalue as individuals if desired.

### 4. PolynomialModel
- **Task:** Polynomial regression on a manufacturing/process dataset
- **Dataset:** Manufacturing Data for Polynomial Regression — https://www.kaggle.com/datasets/rukenmissonnier/manufacturing-data-for-polynomial-regression
- **Notebook:** https://www.kaggle.com/code/rukenmissonnier/master-polynomial-regression-with-this-notebook
- **Alternate (simpler):** Ice Cream Sales vs. Temperature — https://www.kaggle.com/datasets/mirajdeepbhandari/polynomial-regression
- **Why it fits:** Explicit polynomial-degree fitting (not just linear regression) maps directly
  onto PolynomialModel; the "degree selection" step is a good example of a
  MachineLearningParameterInitialization individual.

### 5. NonParametricModel
- **Task:** K-Nearest-Neighbors classification
- **Dataset:** Iris Flower Dataset (classic UCI dataset, 4 features, 3 classes)
- **Notebook:** https://www.kaggle.com/code/prakratisingh2509/knn-classifier-on-iris-dataset
- **Alternate:** https://www.kaggle.com/code/skalskip/iris-data-visualization-and-knn-classification
- **Why it fits:** KNN makes no assumption about the underlying data distribution (the textbook
  definition of non-parametric), and is simple enough to encode fully in one sitting.

## Coverage Summary

| MLLO Model Type | Status | Candidate |
|---|---|---|
| ArtificialNeuralNetwork | Done (2 examples) | BreastMNIST/ResNet18, PathMNIST/CustomNet |
| AssociationRuleModel | Selected | Market Basket Apriori |
| ClusteringModel | Selected | Mall Customer K-Means |
| DimensionalityReductionModel | Selected | Wine PCA |
| PolynomialModel | Selected | Manufacturing Polynomial Regression |
| NonParametricModel | Selected | Iris KNN |

That covers all 6 types, with 5 selected as the primary new targets (per the "5 of 6" instruction)
plus ArtificialNeuralNetwork already done twice over.

## Repository Sources Consulted
- Kaggle (primary source for all 4 new candidates — notebooks + datasets in one place, fast to verify)
- UCI Machine Learning Repository (used to confirm dataset provenance for Wine and Iris)
- Not used this round: Hugging Face, Papers with Code — these skew toward NLP/CV model
  repositories rather than the classical-ML model types needed here (association rules,
  clustering, PCA, polynomial regression, KNN aren't typically hosted as Hugging Face model
  cards). Worth revisiting if a later step needs a 7th/8th example.
