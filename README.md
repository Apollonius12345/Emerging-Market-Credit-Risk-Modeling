# Emerging-Market-Credit-Risk-Modeling
A complete credit risk modeling pipeline built for markets lacking historical default data — simulating real-world lending conditions using proxy labels, interpretability techniques, and a leakage-controlled machine learning approach.
## Project Overview
In markets where financial histories are sparse or unreliable, building robust credit risk models presents a unique challenge. This project simulates such a scenario using 438,000 loan application records, crafting an interpretable, proxy-based scoring system that mimics real-world risk modeling. We combine rule-based profiling with a leakage-free XGBoost pipeline, enabling both transparency and high predictive power.
## Motivation
Traditional credit scoring depends heavily on past repayment behavior. But in emerging or greenfield markets, this information is often incomplete, delayed, or nonexistent. This project explores a forward-thinking alternative:
- Create a surrogate label to distinguish risk categories
- Apply interpretable rules for initial risk signaling
- Train a high-performance ML model without relying on future default data
- Prepare the pipeline to upgrade easily once real outcome data becomes available
## Objecitve
Classify loan applicants into potential high-risk and low-risk groups without using historical default labels.
We focus only on profile and behavioral fields like income, employment duration, dependents, and family structure — simulating how lending startups assess new applicants.
## Methodology
### Feature Engineering
- Converted negative duration features into interpretable metrics: AGE_YEARS, YEARS_EMPLOYED
- Created a rule-based risk indicator using a 5-point system: low income, large household, senior age, many dependents, and unknown occupation
- Assigned a proxy label BAD_CLIENT = 1 for applicants scoring above 0.20 in the rule model
### Exploratory Analysis
- Used KDE plots and lollipop charts to identify visual class separability
- Applied Pearson correlation and Chi-Square testing to uncover predictive relationships across numeric and categorical features
### Data Preprocessing
- Cleaned and standardized fields: dropped IDs, handled missing occupations
- Encoded categorical data: one-hot for multi-class fields, binary mapping for boolean columns
- Final feature matrix: 50+ engineered predictors
## Modelling Pipeline
| Model                      | Description                                                          | AUC Score  |
| -------------------------- | -------------------------------------------------------------------- | ---------- |
| **Logistic Regression**    | Baseline with class weighting                                        | 0.98       |
| **XGBoost (Leakage Demo)** | Included proxy risk label during training (teaches overfitting risk) | 1.00       |
| **Leakage-Free XGBoost**   | Removed data leaks, tuned depth & CV folds                           | **0.9997** |
## Business Policy Simulation
Tested model performance at different thresholds:
- Threshold = 0.30: conservative lending, low default risk
- Threshold = 0.70: aggressive lending, higher risk/reward
## Results Summary
The performance comparison between Logistic Regression and the XGBoost risk model demonstrates the clear advantage of advanced modeling when paired with proxy-based labeling. Despite the absence of real default outcomes, the models show compelling separation between risk classes:
| **Metric** (Target: `Bad = 1`) | **Logistic Regression** | **Leakage-Free XGBoost** |
| ------------------------------ | ----------------------- | ------------------------ |
| **Precision**                  | 0.11                    | 0.97                     |
| **Recall**                     | 0.95                    | 1.00                     |
| **F1-Score**                   | 0.19                    | 0.99                     |
| **ROC AUC**                    | 0.98                    | 0.9997                   |

**Note:** Near-perfect AUC arises due to the deterministic nature of the rule-based proxy label. Performance on actual default data would likely be lower but more representative of real-world model generalization.
## Business Decision Thresholds
To simulate how lenders might use this model in production, we evaluated policy scenarios at varying confidence thresholds:
| **Threshold** | **Precision** | **Recall** | **Risk Strategy**                                                                 |
| ------------- | ------------- | ---------- | --------------------------------------------------------------------------------- |
| **0.30**      | 0.94          | 1.00       | *Risk-Averse:* Capture all potential defaulters, even with higher false positives |
| **0.70**      | 0.99          | 0.997      | *Cost-Conscious:* Minimize false approvals, accept slight recall drop             |

These thresholds allow dynamic risk management — enabling institutions to shift strategies between tight credit control and growth-focused lending, all while staying within explainable and data-backed model limits.
