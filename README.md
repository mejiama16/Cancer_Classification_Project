# Cancer Classification Using The Cancer Genome Atlas (TCGA)

**Course:** STA314: Statistical Methods for ML | University of Toronto  

**Author:** Mariana Garcia Mejia

**Final Score:** 1.00 | **Ranking:** 4/10

## Overview
This project classifies three cancer types — Glioblastoma Multiforme (GBM), 
Lung Squamous Cell Carcinoma (LUSC), and Ovarian Cancer (OV) — from 
high-dimensional gene expression data using the TCGA dataset. The project 
addresses two objectives: accurate cancer classification and identification 
of mislabeled observations in real-world genomic data.

## Dataset
- 886 patient samples, 12,042 gene expression features (log-space)
- 3 classes: GBM (408), OV (348), LUSC (130)
- Known class imbalance and deliberately introduced label noise

## Methods
### Preprocessing
- Variance filtering: top 1,000 most variable genes retained
- 80/20 stratified train/validation split

### Models
| Model | Validation Accuracy | LUSC Recall |
|---|---|---|
| Random Forest | 91.01% | 61.54% |
| PCA + LDA (n=7) | 89.89% | 61.54% |
| XGBoost | 92.13% | 65.38% |

### Mislabeled Observation Detection
Two independent methods were used to identify potentially mislabeled samples:
- **Cleanlab** (Confident Learning via RF OOB probabilities): 70 flagged (9.9%)
- **PCA + LDA** probabilistic detection (threshold = 1/3): 92 flagged (13%)
- **100% overlap** between methods — strongly confirming mislabeled samples
- LUSC most affected: 34/104 samples (32.7%) potentially mislabeled

## Key Findings
- Random Forest achieved **100% test accuracy** on Kaggle, signaling possible
  overfitting of XG Boost.
- Ensemble tree methods are inherently robust to label noise: removing 
  suspicious observations did not improve honest validation performance
- Top predictive genes are biologically meaningful: OLIG2, GFAP (GBM markers), 
  WT1, OPCML (OV markers); notably absent LUSC-specific genes explain 
  the lower recall for this class
