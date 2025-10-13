# ICU Mortality Prediction - Python Implementation

### A Comparative Analysis of Feature Ensembles for ICU Mortality Prediction

---

## Overview

This project applies **machine learning** methods to predict **mortality outcomes of ICU patients**, using a subset of the **MIMIC-III** clinical database. The analysis aims to evaluate how different **feature ensembles** and **classification algorithms** perform in identifying high-risk cases, helping inform triage and care allocation decisions in critical care environments.

The project was developed in **Python** as part of *MET CS677 – Data Science with Python* at Boston University.  
A parallel implementation was also completed in **R** for comparative analysis (see *ICU-Mortality-R* repository).

---

## Dataset

- **Source:** MIMIC-III ICU dataset (via Kaggle)  
- **Records:** 1,177 patient entries  
- **Features:** 49 columns, including demographic, biochemical, and clinical measures  
- **Target Variable:** `outcome` → `0` = survived, `1` = deceased  
- **Preprocessing:**  
  - Minimal cleaning required  
  - Missing values imputed with column means  
  - 37 numerical columns used for feature ensemble analysis  

---

## Methods

Three supervised classification algorithms were implemented and compared:

1. **Logistic Regression**
2. **Gaussian Naïve Bayes**
3. **Random Forest**

The analysis proceeds in two main stages:
- **Full Feature Evaluation:** Train each classifier using all available numerical columns.
- **Feature Ensemble Analysis:** Evaluate all **7,770 unique 3-feature combinations** to identify small ensembles with superior predictive power.

Performance metrics include:
- Accuracy
- True Positive Rate (TPR)
- True Negative Rate (TNR)

---

## Results

| Model | Accuracy (Full) | TPR | TNR | Ensembles Beating Full Model |
|--------|----------------|-----|-----|------------------------------|
| Logistic Regression | 85.6% | — | — | 2,607 |
| Naïve Bayes | 88.3% | 54.7% | 94.0% | 0 |
| Random Forest | 94.9% | 67.4% | 99.6% | 0 |

**Top-performing 3-feature ensemble:**  
`Blood calcium`, `Anion gap`, `Lactic acid` → **87.4% accuracy**

---

## Interpretation

- **Random Forest** outperformed both Logistic Regression and Naïve Bayes, reflecting its ability to model **non-linear feature interactions** and handle **categorical variables** effectively.  
- **Naïve Bayes** underperformed due to its assumption of feature independence, which is not valid for many medical comorbidities.  
- The similarity in top ensemble accuracies across models suggests that the most predictive signals are embedded in the **interactions** between features not included in smaller ensembles.

---

## Visualizations

- **Pair plots** highlighting relationships among top features  
- **Model coefficient plots** for interpretability  
- **Error rate heat maps** for Random Forest hyperparameter tuning (`n_estimators`, `max_depth`)  

---

## Limitations & Future Work

- While 94.9% accuracy is high, the **false negative rate** remains concerning in a medical context.  
- Models lack **clinical interpretability**, which is crucial for healthcare applications.  
- Future improvements could include:
  - Incorporating **additional features and observations**
  - Testing **neural network architectures**
  - Performing **cross-validation** and **hyperparameter optimization**
  - Exploring **explainability techniques** (e.g., SHAP, LIME)

---

## Technologies Used

- **Language:** Python 3  
- **Libraries:** `pandas`, `NumPy`, `scikit-learn`, `matplotlib`, `seaborn`, `itertools`  
- **Environment:** Jupyter Notebook  
- **Dataset Source:** Kaggle / MIMIC-III ICU subset  

---

## Author

**Sachin Mohandas**  
Boston University – MET CS677: Data Science with Python  
Term Project (May 2024)  

---

## Related Work

- **R Implementation:** [ICU-Mortality-R](https://github.com/sachinmohandas1/ICU-Mortality-R)
