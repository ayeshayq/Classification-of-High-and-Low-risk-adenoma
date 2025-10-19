##Classification of High- and Low-Risk Adenoma Using Random Forest and XGBoost##

This project aims to classify high-risk (HRA) and low-risk (LRA) adenoma patients (adenomas that may develop into colorectal cancer) using volatile organic compound (VOC) data and advanced machine learning methods. The goal is to uncover both intrinsic structure in the data (unsupervised learning) and predictive biomarkers that differentiate patient groups (supervised learning). Noise removal, baseline correction and alignment is already done.

Two main analyses were performed:
#1. Unsupervised Dimensionality Reduction 
An unsupervised pipeline was designed to explore the inherent structure in the dataset without using labels. The workflow consisted of the following steps:

a.Initial Approach: An Unsupervised Random Forest (uRF) was first combined with Multidimensional Scaling (MDS) to create a baseline visualization of sample relationships. 
b.Refined Approach (Final Version): The pipeline was improved by integrating uRF with UMAP along with a few changes to the preprocessing:


Scaled ComBat Batch Correction: Corrected for inter-batch variability (using sequencing batch as the batch variable and subgroup as the biological covariate). 
PCA Smoothing: Reduced noise by retaining the 50 most informative principal components.
Z-score Normalization: Ensured comparable feature scales after PCA.
uRF Proximity Matrix: Captured pairwise sample similarities through a random forest trained to distinguish real vs. permuted data. 
UMAP Embedding: Generated a low-dimensional (2D) embedding of the proximity matrix to visualize sample clustering.

→ For each model run, a Silhouette Score is given to measure how well points cluster in their groups.

#2. Supervised Classification
The supervised analysis focused on developing robust classification models to distinguish HRA and LRA samples using VOC features.
Preprocessing and Feature Selection:
Removal of samples with excessive missingness.
Median imputation of missing VOC values.
Filtering of significant VOCs based on Mann–Whitney U tests.
Exclusion of outliers 

NOTE: Two files are provided in this repository.

- 'unsupervised_dimensionality_reduction_final.ipynb': the original, step-by-step notebook from that has URF + MDS and pre processing step for URF+UMAP (Baseline, ComBat, PCA, Z-score) separately. 

- 'uRF_UMAP_pipeline.ipynb' : cleaner version of URF+UMAP with single pipeline, reduced redundancy, and added final quantitative comparison (Silhouette scores) to summarize performance across pipelines.


Modeling Approaches:

a.Random Forest Classifier (RF): Evaluated using: Cross-validation (CV) accuracy, test accuracy, Out-of-bag (OOB) score, ROC-AUC and Feature importance plots.


b.XGBoost Classifier: Evaluated using: CV and test accuracy, feature importance visualization


c.SHAP values for model interpretability and insight into individual VOC contributions for both RF and XGboost.


#Data Availability
The original FORAGI “AMOUNTS” VOC dataset used in this project is not included in this repository due to data privacy considerations. Access to the dataset can be provided upon request.
