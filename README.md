# Telecommunications Customer Churn Data Integration and Analysis

## Project Overview

This project implements a comprehensive data integration, cleaning, exploratory analysis, and machine learning classification system to predict customer churn in a telecommunications company. The goal is to identify customers at risk of leaving the service, enabling proactive retention strategies.

## Team Members

- Diego Armando Polanco Lozano
- Ricardo Andres Chamorro Martinez
- Oscar Munoz Ramirez

## Table of Contents

1. [Problem Description](#problem-description)
2. [Dataset](#dataset)
3. [Project Structure](#project-structure)
4. [Methodology](#methodology)
5. [Key Findings](#key-findings)
6. [Model Performance](#model-performance)
7. [Requirements](#requirements)
8. [Usage](#usage)
9. [Conclusions](#conclusions)

## Problem Description

Customer churn is defined as a customer abandoning the telecommunications service. This represents a critical metric for retention strategies. The project frames the problem as a **supervised binary classification** task where:

- **Target Variable:** Churn (1 = customer left, 0 = customer stayed)
- **Explanatory Variables:** Demographic information, contract details, service usage, and customer satisfaction levels

## Dataset

The project integrates multiple data sources related to telecommunications customers:

### Primary Dataset
- `Telco_customer_churn.csv` - Main customer information (7,043 rows, 33 columns)

### Secondary Datasets
- `CustomerChurn.csv` - Additional customer data
- `Telco_customer_churn_demographics.csv` - Demographic information
- `Telco_customer_churn_location.csv` - Location data
- `Telco_customer_churn_population.csv` - Population statistics
- `Telco_customer_churn_services.csv` - Service subscription details
- `Telco_customer_churn_status.csv` - Customer status information

### Final Integrated Dataset
- **7,043 rows** with **64 consolidated columns** after removing redundancies

## Project Structure

```
Integration-and-Analysis-of-Telecommunications-Customer-Churn-Data/
|-- README.md
|-- Telecom_Churn_Integration_and_Analysis.ipynb
|-- data/
    |-- Telecom_Customer_Churn_Complete.csv
    |-- Telecom_Customer_Churn_FINAL_CLEAN.csv
```

## Methodology

### Step 1: Data Integration

The integration process followed a systematic approach:

1. Identified the main file and six complementary secondary files
2. Standardized headers and joining keys (`Customer ID` and `Zip Code`)
3. Performed **left join** operations to preserve all clients from the main dataset
4. Resolved column collisions by prioritizing base file values
5. Verified key integrity, duplicates, and consistency between datasets
6. Documented the process through automatic audits

### Step 2: Data Cleaning and Transformation

1. **Null Value Handling:**
   - `Churn Category` and `Churn Reason` filled with "Not Applicable"
   - Categorical columns imputed with mode
   - `Total Charges` missing values imputed with 0.0

2. **Data Type Corrections:**
   - Converted `Total Charges` to float
   - Converted `Population` to numeric

3. **Category Standardization:**
   - Replaced "No internet service" and "No phone service" with "No"

4. **Feature Engineering:**
   - Created `Tenure_Group` variable with defined intervals (0-12, 12-24, 24-48, 48-60, >60 months)

5. **Column Removal:**
   - Removed identifiers, redundant columns, and potential data leakage sources

6. **Variable Encoding:**
   - Gender encoded ordinally (Male=1, Female=0)
   - Binary variables (Yes/No) converted to 1/0
   - Multi-class variables encoded using One-Hot Encoding

### Step 3: Exploratory Data Analysis (EDA)

Comprehensive analysis covering:
- Class balance visualization
- Churn rates by contract type, demographics, and services
- Monthly and Total Charges distribution analysis
- Tenure analysis and customer lifecycle patterns
- Service adoption impact on churn
- Payment method and billing analysis
- Correlation matrix for numerical variables

### Step 4: Classification System Implementation

Three classification algorithms were implemented:

1. **Logistic Regression:** Linear, interpretable model suitable for binary classification
2. **Decision Tree:** Captures non-linear relationships and provides interpretable decision rules
3. **Random Forest:** Ensemble model that improves robustness and handles mixed data types

### Step 5: Model Evaluation

- **Cross-Validation:** Stratified 5-fold cross-validation
- **Metrics:** Accuracy, Precision, Recall, F1-score, ROC-AUC
- **Final Evaluation:** Independent test set (20% hold-out)

## Key Findings

### Critical Churn Factors

1. **Contract Type:**
   - Month-to-Month contracts: ~42% churn rate
   - One Year contracts: ~11% churn rate
   - Two Year contracts: ~3% churn rate

2. **Customer Tenure:**
   - First 12 months: ~47-50% churn rate
   - After 24 months: <15% churn rate

3. **Additional Services:**
   - Online Security and Tech Support reduce churn significantly (~40% without vs ~15% with)
   - Device Protection and Online Backup also show protective effects

4. **Payment Methods:**
   - Electronic Check: ~45% churn rate
   - Credit Card/Bank Transfer: ~15-17% churn rate

5. **Demographics:**
   - Senior Citizens without Partners/Dependents show highest churn rates (~41-45%)

### Business Recommendations

1. Implement intensive onboarding programs for the first 6-12 months
2. Offer incentives for long-term contracts
3. Bundle security services (Online Security, Tech Support) as essential packages
4. Create high-risk customer segmentation for proactive retention
5. Review pricing structure for Fiber Optic services
6. Develop loyalty programs targeting senior citizens

## Model Performance

### Cross-Validation Results (5-Fold)

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|-------|----------|-----------|--------|----------|---------|
| Logistic Regression | 0.958 | 0.938 | 0.902 | 0.919 | 0.992 |
| Decision Tree | 0.942 | 0.888 | 0.896 | 0.892 | 0.928 |
| Random Forest | 0.957 | 0.971 | 0.864 | 0.914 | 0.984 |

### Final Test Set Results (Random Forest)

- **Accuracy:** 0.953
- **Precision (Churn):** 0.970
- **Recall (Churn):** 0.850
- **F1-score (Churn):** 0.906
- **AUC-ROC:** 0.981

### Selected Model

**Random Forest** was selected as the best model due to:
- Excellent balance between precision and recall
- High discriminative capacity (AUC = 0.98)
- Robustness against noise and variable interactions
- Strong generalization performance

## Requirements

```
pandas
numpy
matplotlib
seaborn
scikit-learn
```

## Usage

1. Clone the repository
2. Ensure the data files are in the correct directory structure
3. Open and run the Jupyter notebook `Telecom_Churn_Integration_and_Analysis.ipynb`
4. The notebook will generate:
   - Integrated dataset: `data/Telecom_Customer_Churn_Complete.csv`
   - Final clean dataset: `data/Telecom_Customer_Churn_FINAL_CLEAN.csv`

## Conclusions

This project successfully demonstrated:

1. **Data Integration:** Systematic unification of multiple data sources into a coherent master dataset
2. **Data Quality:** Comprehensive cleaning and transformation ensuring data consistency
3. **Exploratory Analysis:** Deep insights into churn patterns and risk factors
4. **Predictive Modeling:** High-performance classification system capable of identifying at-risk customers

The Random Forest model achieves superior overall performance with an adequate balance between precision and recall. This model can serve as an effective tool to anticipate customer defection, optimize retention strategies, and improve decision-making in telecommunications companies.

### Limitations and Future Work

- Explore resampling techniques (SMOTE) to address class imbalance
- Implement hyperparameter optimization (GridSearchCV, RandomizedSearchCV)
- Evaluate additional ensemble models (XGBoost, LightGBM)
- Apply explainability techniques (SHAP, LIME) for model interpretation
- Develop automated preprocessing and validation pipelines
