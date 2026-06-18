Candidate Datasets and Models

## Target MLLO Model Types (5 of 6)
1. ArtificialNeuralNetwork
2. NonParametricModel
3. PolynomialModel
4. ClusteringModel (pending Serm confirmation)
5. DimensionalityReductionModel (pending Serm confirmation)

## Candidate List

### Medical Imaging (MedMNIST)

1. **PathMNIST**: Colon pathology image classification, 9 classes. Best model: ResNet-50. MLLO type: ArtificialNeuralNetwork.
https://medmnist.com/ 

2. **ChestMNIST**: Chest X-ray multi-label classification, 14 diseases. Best model: ResNet-18. MLLO type: ArtificialNeuralNetwork.
https://medmnist.com/

### Drug Discovery (TDC)

3. **TDC.BBB_Martins**: Blood-brain barrier penetration prediction. Best model: MiniMol. MLLO type: ArtificialNeuralNetwork.
https://tdcommons.ai/benchmark/admet_group/07bbb/

4. **TDC.DILI**: Drug-induced liver injury prediction. Best model: MapLight+GNN. MLLO type: NonParametricModel.
https://tdcommons.ai/benchmark/admet_group/22dili/

5. **TDC.Clearance_Hepatocyte_AZ**: How fast the liver clears a drug. Best model: RFStacker. MLLO type: NonParametricModel.
https://tdcommons.ai/benchmark/admet_group/17clhepa/

6. **TDC.PPBR_AZ**: Plasma protein binding rate. Best model: Chemprop-RDKit. MLLO type: PolynomialModel.
https://tdcommons.ai/benchmark/admet_group/08ppbr/

7. **TDC.VDss_Lombardo**: Drug distribution volume in the body. Best model: Chemprop-RDKit. MLLO type: PolynomialModel.
https://tdcommons.ai/benchmark/admet_group/09vdss/

### Healthcare (UCI)

8. **Breast Cancer Wisconsin**: Tumor malignancy classification. Best model: SVM. MLLO type: NonParametricModel.
https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic

9. **Heart Disease**: Heart disease prediction. Best model: Logistic Regression. MLLO type: PolynomialModel.
https://archive.ics.uci.edu/dataset/45/heart+disease

10. **Chronic Kidney Disease**: Kidney disease classification. Best model: Random Forest. MLLO type: NonParametricModel.
https://archive.ics.uci.edu/dataset/336/chronic+kidney+disease

##  Domains
- MedMNIST
- Drug discovery / ADMET (TDC)
- Clinical healthcare (UCI)

## Notes
- Pete's already done work: TDC HIA_Hou, TDC Solubility_AqSolDB, PharmaBench AMES, IndPenSim, SubstrateMixRaman
