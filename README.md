# Part 3 — Churn Prediction Model & Model Card

D2C Customer Churn Capstone. Predicts whether a customer churns in the 60 days after
the snapshot (2025-09-30).

## How to run
1. Open `churn_model.ipynb` in Google Colab (or Jupyter).
2. Upload `rfm_modeling_snapshot.csv` (the pre-engineered, leakage-safe feature table).
3. Run all cells. It saves `model.pkl` and `metrics.json`.

## Approach
- Features: all columns in the modelling table except IDs, target, and split.
  The target (`churn_next_60d`) is asserted out of the feature set (leakage guard).
- Split: the provided `split` column (train 1728 / val 336 / test 336).
- Models: Logistic Regression (baseline) vs tuned HistGradientBoosting (stronger).
- Metrics: ROC-AUC, PR-AUC, precision, recall, F1 — not accuracy alone (target ~47% churn).
- Threshold: chosen below 0.5 to favour recall, because missing a churner costs more
  than a wasted low-cost campaign.

## Reference results (will vary slightly on your run)
- Validation ROC-AUC ~0.88 for both models (recency dominates the signal).
- Test @ threshold 0.40: recall ~0.85, precision ~0.75.

## Outputs
- `churn_model.ipynb`
- `model.pkl` (pipeline + threshold + feature columns)
- `metrics.json`
- `error_analysis.md`
- `model_card.md`
