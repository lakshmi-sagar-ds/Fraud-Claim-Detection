# Fraudulent Claim Detection for Insurance Claims

## ✅ Objective  
The objective of this project was to help **Global Insure**, an insurance company, detect **fraudulent insurance claims early in the approval process** using historical claim and customer data.  
At the time, fraud detection relied heavily on **manual inspections**, which were slow and often identified fraud only after payouts had occurred. The goal was to build a **classification model** to flag potentially fraudulent claims before approval, reducing financial losses and improving operational efficiency.

---

## 📊 About the Data  
The dataset consists of **1,000 insurance claim records** with **40 attributes**, covering customer demographics, policy details, incident characteristics, and claim amounts.

- **Target Variable:** Fraud Reported (Fraudulent / Legitimate)
- **Fraud Rate:** ~24% fraudulent claims (class imbalance present)
- **Feature Types:**
  - Customer profile (age, tenure, premiums)
  - Policy and coverage details
  - Incident and claim-related information
  - Financial claim components (vehicle, injury, property)

---

## Data Cleaning & Preprocessing  

- Replaced missing values in categorical fields such as `authorities_contacted` with `"Unknown"`
- Dropped columns with complete null values (e.g., `_c39`)
- Standardised ambiguous entries (e.g., `"?"` → `"Unknown"`)
- Removed high-cardinality or non-informative identifiers: Policy number, ZIP code, vehicle details, incident location
- Converted date columns to proper datetime formats
- Corrected data types (e.g., annual premium from float to integer)
- Addressed **class imbalance** using **Random Oversampling**
- Applied **One-Hot Encoding** for categorical variables
- Scaled numerical features using **StandardScaler**

---

## Feature Selection  

- Identified correlations between features such as **age** and **months as customer**
- Used:
  - **RFECV** for Logistic Regression feature selection
  - **Feature importance scores** for Random Forest
- Removed redundant date-derived features that did not add predictive value
- Retained features with strong predictive and business relevance

---

## 📈 Exploratory Data Analysis (EDA)  

Key observations from EDA:

- Fraudulent claims are more common among **newer customers**
- Fraud tends to cluster around:
  - Specific **premium ranges**
  - **Higher total claim amounts**
- Fraud cases often show inflated:
  - Injury claims
  - Vehicle repair costs
  - Property damage amounts
- Certain **age groups (30–40)** exhibit higher fraud incidence
- Fraud claims are more frequent during **specific reporting hours**
- Heatmaps revealed non-random associations between policy attributes and fraud

---

## Model Building  

Two classification models were built and compared:

### Logistic Regression
- Used for interpretability and feature-level insights
- Base model showed signs of **overfitting**
- Feature selection and hyperparameter tuning applied
- **Final test accuracy:** ~81%
- **Fraud capture (recall):** ~66%

### Random Forest
- Built as a comparative non-linear model
- Feature importance used for selection
- Tuned model achieved lower generalisation performance than Logistic Regression

**Final Model Selection:**  
Logistic Regression was chosen due to **better interpretability and stable performance**.

---

## 🔑 Key Fraud Indicators Identified  

- **Short customer tenure** is strongly associated with fraud risk
- Certain cost thresholds attract higher fraud:
  - Policy deductible
  - Annual premium
  - Umbrella coverage limits
- Fraudulent claims frequently inflate:
  - Total claim amount
  - Vehicle, injury, and property components
- Incident type is one of the most predictive features

---

## Recommendations  

- Apply **additional scrutiny to short-tenure customers**
- Introduce tighter checks around:
  - High deductibles
  - Premium and umbrella limit thresholds
- Flag claims with unusually high or bundled cost components
- Use model outputs to **prioritize manual reviews**, not replace them

---
