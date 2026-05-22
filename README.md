# Online Shoppers' Purchasing Intention | Behavioural Analytics | R

## Project Overview
Analysed 12,000+ e-commerce sessions from the UCI Online Shoppers Purchasing Intention dataset to identify behavioural drivers of purchase conversion. Conducted hypothesis testing, correlation analysis, and built three classification models — Logistic Regression, Decision Tree, and Random Forest — alongside an exploratory linear regression on page engagement.

## Tools & Technologies
- **Language:** R / RStudio
- **Visualisation:** ggplot2, corrplot
- **Modelling:** caret, rpart, randomForest, pROC
- **Data Wrangling:** dplyr

## Dataset
UCI Machine Learning Repository — *Online Shoppers Purchasing Intention Dataset* (Sakar & Kastro, 2018). Single-table dataset with 12,330 observations and 18 variables covering session behaviour, product-related interactions, technical attributes, and a binary `Revenue` target. No missing values.

> Source: Sakar, C. & Kastro, Y. (2018). [Online Shoppers Purchasing Intention Dataset](https://doi.org/10.24432/C5F88Q). UCI Machine Learning Repository.

## Key Findings
- **PageValues is the strongest revenue predictor** — Pearson r ≈ 0.49 (p < 2.2e-16); users engaging with high-value pages are significantly more likely to convert
- **Special days negatively correlate with conversions** — contrary to behavioural economics intuition, proximity to special occasions is associated with browsing rather than purchase intent (mean SpecialDay: 0.068 for non-revenue vs 0.023 for revenue sessions)
- **Traffic source has a statistically significant but weak effect** on revenue (χ² = 373.15, p < 2.2e-16), with TrafficType emerging as non-significant in logistic regression
- **Decision tree flagged a 75% conversion likelihood** for users with PageValues > 23, enabling tiered behavioural segmentation
- **All three classifiers achieved ~88% accuracy**, with high sensitivity (~95%) for non-revenue users but lower specificity (~33–53%) for revenue users — reflecting class imbalance; Logistic Regression AUC = 0.8592

## Methodology Summary
1. **Preprocessing & EDA** — factor conversion for categorical variables; correlation heatmap, boxplots, and bar plots to surface behavioural patterns
2. **Hypothesis Testing**
   - H1: PageValues vs Revenue — Pearson correlation test
   - H2: SpecialDay vs Revenue — Welch two-sample t-test
   - H3: TrafficType vs Revenue — Chi-square test of independence (with simulated p-value)
3. **Classification Models** — Logistic Regression (AUC = 0.8592), Decision Tree (tiered PageValues segmentation, accuracy = 88.27%), and Random Forest (feature importance confirms PageValues dominance, accuracy = 88.24%)
4. **Exploratory Linear Regression** — predicted PageValues from ExitRates, BounceRates, and ProductRelated_Duration; R² = 3.9%, highlighting latent behavioural complexity beyond observable session metrics

## Model Performance Summary

| Model               | Accuracy | AUC    | Sensitivity | Specificity | Kappa  |
|---------------------|----------|--------|-------------|-------------|--------|
| Logistic Regression | 87.7%    | 0.8592 | 97.7%       | 33.3%       | —      |
| Decision Tree       | 88.27%   | —      | 94.69%      | 53.31%      | 0.5175 |
| Random Forest       | 88.24%   | —      | 94.91%      | 51.92%      | 0.5108 |

## Limitations & Extensions
- Class imbalance (~84% non-revenue sessions) suppresses specificity across all models — **SMOTE or class-weight adjustment** is a natural next step
- Low R² in linear regression (3.9%) suggests PageValues is driven by latent qualitative factors not captured in the dataset
- **XGBoost or regularised regression** could improve discrimination for the minority (revenue) class
- Incorporating clickstream depth, referral quality, and device type may meaningfully boost specificity
