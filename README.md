# 💳 Credit Card Expenditure Prediction

## 📘 Introduction

This project investigates the factors that influence individual credit card expenditures using data from **Kaggle’s Credit Card dataset** (originally from *Econometric Analysis*). The analysis focuses on understanding how demographic and financial characteristics — such as **income, age, dependents, and credit rating measures** — affect monthly spending behavior.

We employ **multiple linear regression modeling in R** to identify the strongest predictors of credit card expenditure, explore variable interactions, and test key model assumptions. The project’s goal is to produce a statistically sound, interpretable, and predictive model for expenditure estimation.

---

## 🎯 Purpose

Financial institutions and consumers alike can benefit from insights into what drives spending. By modeling these relationships, we aim to:

* Identify the **most influential predictors** of monthly credit card expenditure.
* Examine whether **demographic and credit history variables** interact to affect spending.
* Build a model that balances **accuracy, simplicity, and generalizability**.

---

## 🔍 Data Overview

The dataset includes variables such as:

* **Expenditure:** Average monthly credit card expenditure
* **Income:** Annual income of the cardholder
* **Share:** Ratio of monthly credit card expenditure to yearly income
* **Dependents:** Number of dependents
* **Months, Active:** Duration and number of active credit card accounts
* **Major Derogatory Reports, Self-employment, Homeownership**, etc.

---

## 📊 Exploratory Data Analysis (EDA)

* **Skewness:** Expenditure, share, and months were right-skewed with outliers.
* **Correlation:** *Share* had the strongest correlation with *expenditure* (r = 0.83).
* **Patterns:** Homeowners spent more than renters; individuals with derogatory reports spent less.
* **Data Cleaning:** Removed invalid and outlier observations (e.g., 0 dependents or zero expenditure).

---

## 🧮 Modeling Process

### 1. Initial Model

**Model:**
`expenditure ~ income + share + dependents + months + active`

* Training Adjusted R² = **0.7962**
* Testing Adjusted R² = **0.848**
* RMSE = **101.7**
  Despite strong performance, residual plots revealed **heteroskedasticity** and **non-normal residuals**.

---

### 2. Transformations & Feature Engineering

To improve linear regression assumptions:

* **Box–Cox Transformation (λ = 0.5)** on `expenditure`
* **Square-root Transformation** on `share` to reduce skewness
* **Interaction Term:** `√share × dependents` added after identifying its statistical significance (F ≈ 40.45, p < .001)

---

### 3. Model Simplification

Removed non-significant predictors (*income, months, active*) using partial F-tests.
Retained:

* `√share`
* `dependents`
* `√share × dependents` (interaction)

---

## 🧠 Final Model

**Model Formula:**
[
\sqrt{\text{expenditure}} = 1.3297 + 40.6148(\sqrt{\text{share}}) - 0.5161(\text{dependents}) + 6.8362(\sqrt{\text{share}} \times \text{dependents})
]

**Performance Metrics:**

* Training Adjusted R² = **0.8391**
* Testing Adjusted R² = **0.7153**
* RMSE = **4.34**

This model achieved a strong fit and predictive accuracy while maintaining interpretability.

---

## 🔍 Model Diagnostics

* ✅ **Independence:** Passed (Durbin–Watson test)
* ⚠️ **Normality & Constant Variance:** Still violated due to inherent heteroskedasticity
* Despite assumption failures, **predictive performance remained robust** — acceptable since the focus is prediction, not inference.

---

## 🏁 Conclusion

The final model effectively predicts credit card expenditure using transformed variables and a meaningful interaction between **share** and **dependents**.
Key takeaways:

* **Share** (credit usage ratio) is the most dominant predictor of expenditure.
* Interaction with **dependents** suggests spending behavior scales differently across family sizes.
* Despite some residual assumption violations, the model is **accurate, interpretable, and generalizable** for predictive purposes.

### Limitations

* Skewed distributions and heteroskedasticity limit perfect adherence to regression assumptions.
* The dataset lacks behavioral or temporal features that could further refine prediction accuracy.

---

## 🧰 Tools & Libraries

* **R Packages:** `car`, `FSA`, `ggplot2`
* **Techniques:** EDA, Multiple Linear Regression, Box–Cox Transformation, Interaction Terms, Model Validation

---

## 📈 Future Work

* Incorporate **nonlinear models** (e.g., Random Forest or Gradient Boosting) for comparison.
* Experiment with **robust regression** to mitigate heteroskedasticity.
* Expand feature set to include **spending categories** or **credit utilization history**.
