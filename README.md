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

