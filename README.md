# ⚡ Electricity Cost Analysis in Oregon
**Cindy Chen**  
**Date:** March 9, 2024  

---

## 📌 Overview

This project uses American Community Survey (ACS) microdata to analyze electricity costs at the household level in Oregon. The goals are twofold:

- 🧠 **Explanatory Analysis:** Do apartment residents pay less for electricity than house residents, after adjusting for confounders like number of bedrooms and occupants?
- 🔮 **Predictive Modeling:** Build a model to accurately predict monthly electricity expenditure (`ELEP`) based on household and demographic features.

---

## 📊 Dataset

- **Source:** `OR_acs_house_occ.csv`
- **Scope:** Households in Oregon
- **Key Features:**
  - `ELEP`: Electricity cost (response variable)
  - `HFL`: Housing/fuel type
  - `NP`: Number of people in household
  - `BDSP`: Number of bedrooms
  - `RMSP`, `VALP`, `FULP`, `GASP`, `R18`: Additional housing & demographic features

---

## 🧹 Data Preprocessing

- 🔧 **Missing Values:**
  - Imputed mean (numeric) and mode (categorical)
- 🏠 **Housing Type Cleanup:**
  - `HFL` → `Cleaned_HFL`: Categorical, binary (Electricity vs. Non-Electricity)
- 🧭 **Exploration:**
  - Boxplots & scatterplots for key relationships
  - Correlation matrix to assess linear associations

---

## 📐 Modeling Strategy

Three models were developed:

| Model | Type                         | Description                                                    |
|-------|------------------------------|----------------------------------------------------------------|
| 1     | Multiple Linear Regression   | Baseline with `NP`, `Cleaned_HFL`, `BDSP`                      |
| 2     | Extended Linear Regression   | Adds `FULP`, `GASP`, `RMSP`, `VALP`, `R18`                     |
| 3     | Generalized Linear Model     | GLM with Gaussian family & identity link                       |

---

## 📈 Exploratory Insights

- Houses tend to have **higher electricity costs** than apartments.
- **More people** → more stable electricity costs in houses.
- In apartments, cost varies more with number of bedrooms.
- **Key correlated features**: `NP`, `VALP`, `RMSP`, and fuel type.

---

## 📊 Model Performance

Model comparison (on validation set):

| Metric       | Model 1 | Model 2 (Best) | Model 3 |
|--------------|---------|----------------|---------|
| MSE          | High    | 🔽 Low         | Medium  |
| MAE          | High    | 🔽 Low         | 🔽 Low  |
| Adjusted R²  | 0.154   | **0.188**      | 0.185   |
| AIC/BIC      | Higher  | ✅ Lowest      | Medium  |

- 🔬 **Model 2 wins**: Best trade-off between fit, interpretability, and accuracy.
- ✅ Strongest explanatory power with statistically significant predictors.
- 🧪 Validated via F-test against baseline.

---

## 🔁 Explanatory vs. Predictive Approaches

| Aspect             | Explanatory Analysis              | Predictive Modeling               |
|--------------------|-----------------------------------|-----------------------------------|
| **Goal**           | Understand drivers of `ELEP`      | Accurately forecast `ELEP`        |
| **Key Methods**    | Regression & diagnostics          | Train-test split, error metrics   |
| **Focus**          | Statistical significance          | Generalization error              |
| **Outcome**        | Insights on housing/electricity   | Deployed model for forecasting    |

---

## 🧠 Conclusions

- Apartments typically incur **lower electricity costs**, even after adjustments.
- **Model 2** (extended linear regression) performed best in both accuracy and insight.
- Electricity cost is impacted by **housing type, fuel type, occupancy**, and **valuation metrics**.

---

## 🚀 Future Directions

- Explore **interaction effects** (e.g., housing type × occupancy)
- Apply **non-linear models** (Random Forest, XGBoost)
- Extend analysis to **other U.S. states** or **year-over-year trends**

---

## 📁 Repo Contents

```plaintext
├── data/
│   └── OR_acs_house_occ.csv
├── scripts/
│   ├── data_cleaning.R
│   ├── model_fitting.R
│   └── exploratory_analysis.R
├── figures/
│   ├── elep_by_housing_type.png
│   └── correlation_matrix.png
├── report/
│   └── Electricity_Cost_Report.pdf
├── README.md
