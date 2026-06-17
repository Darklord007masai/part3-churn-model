# Deep-Dive Error Analysis & Threshold Optimization

## 1. Mathematical Threshold Justification
* [cite_start]Explain the trade-offs of using a `0.35` decision threshold. 
* [cite_start]A False Positive costs a small marketing retention discount, whereas a False Negative costs the lifetime value (LTV) of an entirely lost customer[cite: 75].

## 2. Granular Evaluation Matrix (10 Customer Case Examples)
[cite_start]Analyze 10 real sample IDs that your model struggled to categorize correctly[cite: 75]. Use this precise layout:

### Case 1: The Active Complainer (False Positive)
* **Customer ID**: CUST-1092
* **Model Prediction Probability**: 78% risk (Classified as Churn)
* **Actual Label**: 0 (Retained)
* **Root-Cause Analysis**: The customer logs massive web sessions and order frequencies, but opened 3 support tickets right before the snapshot date. The model over-indexed on ticket friction, failing to realize the high baseline app engagement kept them loyal.

### Case 2: The Silent Churner (False Negative)
* **Customer ID**: CUST-4412
* **Model Prediction Probability**: 14% risk (Classified as Retained)
* **Actual Label**: 1 (Churned)
* **Root-Cause Analysis**: This customer had pristine engagement metrics up to the snapshot date (0 tickets, standard spend), but abruptly stopped purchasing without warning signals. This represents a limitation of purely historical feature summaries.
