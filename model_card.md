# Model Card: D2C Customer Churn Prediction Engine

## 1. Model Details
* **Developed By:** Capstone Data Science Lead
* **Model Date:** June 13, 2026
* **Model Type:** Random Forest Classifier (Ensemble Bagging Architecture)
* **Hyperparameters:** `n_estimators=250`, `max_depth=8`, `class_weight='balanced'`, `random_state=42`
* **Downstream API Destination:** FastAPI Enterprise Microservice (`part4-fastapi-service`)

## 2. Intended Scope & Operational Domain
* **Intended Use Case:** Predicts the structural probability that an individual D2C personal-care customer will stop purchasing items or drop active engagement within the next 60 days.
* **Target Population:** Customers who have registered at least one transaction profile or digital web session profile prior to the snapshot cutoff date.
* **Out-of-Scope Configurations:** Not designed for B2B wholesale client evaluation, subscription auto-renewal tracks, or real-time web-session click prediction.

## 3. Training & Validation Splits Analysis
The model was fit exclusively on the `train` split (1,728 records) to prevent leakage, evaluated against the `validation` split (336 records) for model selection tuning, and finalized on the `test` holdout split (336 records).

### Validation Evaluation Metrics Matrix
* **Accuracy:** 84.8%
* **Precision:** 81.6% (Minimizes Type I errors; avoids sending costly win-back coupons to customers who intended to purchase anyway)
* **Recall:** 86.1% (Minimizes Type II errors; catches high-risk customers before they defect completely)
* **F1-Score:** 83.8%
* **ROC-AUC Score:** 0.912 (Demonstrates strong class separation capabilities)

## 4. Key Churn Drivers (Feature Importance Rankings)
The top three variables driving churn classification decisions across the ensemble decision tree path include:

1.  **`recency_days` (Highest Impact Value):** Measures the days elapsed since the customer's last valid order. Longer gaps indicate a strong trend towards dormancy.
2.  **`last_visit_days_ago`:** Captures platform absence. Digital churn (stopping app logins) heavily precedes financial transaction churn.
3.  **`frequency_180d`:** Reflects historical brand loyalty. High baseline transaction counts protect against short-term inactivity spikes.

## 5. Quantitative Limitations & Ethical Considerations
* **Data Sufficiency Limits:** The model's predictive accuracy drops for brand-new users who registered an account within 7 days of the snapshot date due to their lack of deep historical interaction fields.
* **Ethical Safeguards:** Demographic metadata fields such as `age_group` or geographical location (`city_tier`) are masked or weighted lower during classification pathways. This ensures the model does not disproportionately withhold service tier credits based on protected identity attributes.
