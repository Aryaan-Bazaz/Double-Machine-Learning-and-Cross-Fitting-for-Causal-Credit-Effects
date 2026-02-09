# Double Machine Learning and Cross-Fitting for Causal Credit Effects

This repository contains the project **“Double Machine Learning and Cross-Fitting for Causal Credit Effects”**, which applies modern causal machine learning methods to estimate the causal impact of agricultural credit on crop yields in India.

**Authors**: Aryaan Bazaz, Parth Rastogi  
**Affiliation**: Indraprastha Institute of Information Technology Delhi  
**Data**: Indian sorghum farmers (2001–2014)  
**Methods**: Double/Debiased Machine Learning, Cross-Fitting, Meta-Learners  

📄 Full project report: *Double Machine Learning and Cross Fitting for Causal Credit Effects* :contentReference[oaicite:0]{index=0}

---

## Motivation

Access to agricultural credit is central to productivity and food security, yet estimating its **true causal effect** is challenging due to selection bias and high-dimensional confounding.

Farmers who receive credit differ systematically from those who do not (soil quality, ability, risk tolerance). Naive regressions and matching approaches overstate effects, while flexible ML methods introduce **regularization bias** and invalidate inference.

This project uses **Double/Debiased Machine Learning (DML)** with **cross-fitting** to obtain unbiased treatment effect estimates with valid confidence intervals.

---

## Research Questions

1. Does Double Machine Learning change estimated credit effects relative to baseline methods?
2. How does cross-fitting improve robustness and inference?
3. How do formal and informal credit differ in their causal impact on yields?
4. Do heterogeneous treatment effect learners confirm average effect estimates?

---

## Data

- **Observations**: ~2,151 farm-year observations  
- **Period**: 2001–2014 (unbalanced panel)  
- **Outcome**: Sorghum yield (kg/acre)  
- **Treatments**:
  - `DITF`: Formal credit
  - `DITI`: Informal credit
- **Covariates**:
  - Land & soil characteristics
  - Fertilizer, irrigation, and management inputs
  - Socioeconomic and caste variables
  - Village and year fixed effects

Missing values are handled via mean (continuous) and mode (categorical) imputation.

---

## Methodology

### Baseline Approaches
- Propensity Score Matching (PSM)
- Logistic regression (standard, scaled, L1)
- Decision tree propensity models
- Panel fixed effects

These methods suffer from imbalance, sensitivity to hidden bias, and regularization-induced bias.

---

### Double Machine Learning (DML)

- Orthogonal score construction removes regularization bias
- Separates nuisance estimation from treatment effect estimation
- Enables valid inference with flexible ML models

**Nuisance models**:
- Propensity score: Logistic Regression, Random Forest
- Outcome model: Linear Regression, Random Forest

---

### Cross-Fitting

- 5-fold sample splitting
- Prevents overfitting in nuisance estimation
- Ensures correct standard errors and confidence intervals

---

### Extensions: Heterogeneous Treatment Effects

Meta-learners implemented using Random Forests:
- S-Learner
- T-Learner
- X-Learner
- DR-Learner
- D-Learner

Each estimator reports:
- Individual treatment effects
- Average Treatment Effect (ATE)
- Average Treatment Effect on the Treated (ATT)

---

## Key Results

### Baseline Models
- Logistic PSM performs better than tree-based PSM
- Tree-based propensity models exhibit poor balance and low robustness
- Results are highly model-dependent

---

### DML Results
- Logistic-DML (no interaction terms) provides the most stable estimates
- Interaction-heavy models degrade balance and violate DML assumptions
- Random Forest DML improves overlap but remains sensitive without cross-fitting

---

### Meta-Learner Results (Most Robust)

**Formal Credit (DITF)**:
- Positive and statistically significant effect
- ATE: +13 to +29 kg
- ATT: +11 to +25 kg
- Strong evidence of productivity gains

**Informal Credit (DITI)**:
- Negative and statistically significant effect
- ATE: –5 to –16 kg
- ATT: –9 to –14 kg
- Suggests distress borrowing rather than productive investment

Results are consistent across X-, S-, and T-learners, strengthening causal interpretation.

---

## Interpretation

- Formal credit improves agricultural productivity
- Informal credit is associated with lower yields
- DML corrects upward bias present in baseline estimates
- Heterogeneous ML estimators provide the most stable inference

---

## Repository Structure

