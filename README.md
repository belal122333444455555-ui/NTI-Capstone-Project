# 🦷 Dental Health Risk Assessment: Periodontitis Prediction Model

An automated clinical screening tool and machine learning pipeline for predicting patient risk of **Periodontitis** using health survey data from the **National Health and Nutrition Examination Survey (NHANES)**. 

This project aims to provide non-invasive clinical and medical risk assessments to enable early intervention and preventative dental care.

---

## 📌 Executive Overview

Periodontitis is a severe gum infection that damages soft tissue and can destroy the bone that supports teeth. Early detection is critical for effective management. 

Using non-invasive medical indicators, demographics, and oral hygiene measurements from NHANES, this project builds and compares multiple Machine Learning models to classify patients into risk categories, selecting the best model for real-time risk assessment in clinical settings.

---

## 🛠️ Tech Stack & Dependencies

* **Language:** Python 3.10+
* **Data Manipulation & Analysis:** `pandas`, `numpy`
* **Machine Learning & Modeling:** `scikit-learn`
  * `LogisticRegression`
  * `GradientBoostingClassifier`
  * `RandomForestClassifier`
* **Data Preprocessing:** `SimpleImputer`, `StandardScaler`, `VarianceThreshold`
* **Visualization:** `matplotlib`

---

## 🔄 Data Pipeline & Preprocessing

The dataset was carefully preprocessed to remove noise, eliminate target leakage, and handle high-dimensional survey features:

1. **Feature Selection & Cleaning:**
   * Filtered out unneeded administrative/survey weights (e.g., `WTINT2YR`, `SDMVPSU`, `SEQN`) to prevent target leakage.
   * Dropped columns with greater than **50% missing values**.
2. **Missing Data Imputation:**
   * Used `SimpleImputer(strategy='median')` to handle remaining missing clinical variables robustly against skewed data and outliers.
3. **Encoding & Multicollinearity Removal:**
   * Categorical features (such as `RIAGENDR`) were converted and encoded using One-Hot Encoding (`pd.get_dummies`).
   * Applied `VarianceThreshold(threshold=0.0)` to eliminate constant (zero-variance) features, reducing redundant features from **384 to 340**.
4. **Data Splitting & Feature Scaling:**
   * Stratified **80/20 Train-Test Split** (`stratify=y`) to maintain class balance across training and test sets.
   * Features were standardized using `StandardScaler` for distance/linear models.

---

## 📊 Model Benchmarking & Architecture

Three distinct classification architectures were evaluated:

| Model | Role & Description |
| :--- | :--- |
| **Logistic Regression** | Interpretable linear baseline model. |
| **Gradient Boosting Classifier** | Sequential boosting architecture to capture non-linear feature relationships. |
| **Random Forest Classifier** *(Selected)* | Ensemble bagging model aggregating decorrelated decision trees. |

### 🏆 Selected Model: Random Forest Classifier
The **Random Forest Classifier** was selected as the optimal model for deployment. By aggregating multiple decision trees, it demonstrated:
* Highest overall performance across key metrics (**Accuracy, Precision, Recall, Macro F1-Score, and ROC-AUC**).
* Superior handling of non-linear feature interactions without overfitting.
* Low variance and strong generalization performance on unseen test data.

---

## 🚀 Future Deployment Strategy

The trained **Random Forest model** is designed to be integrated into a lightweight **Streamlit Web Application**. This will allow healthcare providers and clinicians to:
1. Input patient demographic and non-invasive medical parameters.
2. Receive instantaneous, real-time risk predictions for Periodontitis.
3. Provide timely recommendations and referrals for preventative dental procedures.

---

## 💻 How to Run the Project

1. **Clone the repository:**
   ```bash
   git clone  (https://github.com/belal122333444455555-ui/NTI-Capstone-Project.git)
