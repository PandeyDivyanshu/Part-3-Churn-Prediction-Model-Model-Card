# Model Card - Churn Prediction (60-day)

## 1) Intended Use
- Support retention prioritization for CRM workflows.
- Not for punitive actions or customer exclusion.

## 2) Data Used
- Source: rfm_modeling_snapshot.csv (pre-built feature table, leakage-free)
- Snapshot date: 2025-09-30
- Target: churn_next_60d (1 = no purchase Oct-Nov 2025)
- Train/Val/Test split: Pre-defined in data

## 3) Model Approach
- Baseline: Logistic Regression (for comparison)
- Final model: Gradient Boosting Classifier
  - n_estimators=300, max_depth=4, learning_rate=0.05
  - class_weight balanced for imbalanced data
  - Features: 19 numeric + 6 categorical (25 total)

## 4) Performance (Test Set)

| Metric | Value |
|---|---:|
| Accuracy | 0.7887 |
| Precision | 0.7487 |
| Recall | 0.8690 |
| F1-Score | 0.8044 |
| ROC-AUC | 0.8577 |
| PR-AUC | 0.8283 |
| Selected Threshold | 0.40 |

Confusion Matrix (at threshold=0.40):
| | Predicted No-Churn | Predicted Churn |
|---|---:|---:|
| Actual No-Churn (0) | 119 (TN) | 49 (FP) |
| Actual Churn (1) | 22 (FN) | 146 (TP) |

**Threshold Rationale:** 0.40 selected to maximize recall (catch churners)
while maintaining precision > 0.50 (avoid wasting retention budget).

## 5) Key Features
Top 5 most important features:
| Feature | Importance |
|---|---:|
| recency_days | 0.5082 |
| monetary_180d | 0.0999 |
| days_since_signup | 0.0528 |
| product_views_30d | 0.0484 |
| last_visit_days_ago | 0.0472 |

## 6) Limitations
- Sensitive to seasonality and campaign policy changes.
- May underperform on new customer cohorts with short history.
- Does not capture external events (competitor actions, macro shifts).
- Based on historical behavior; may not predict unprecedented changes.

## 7) Ethical & Operational Risks
- Risk of over-targeting vulnerable customers with aggressive nudges.
- Risk of bias if service-quality differences are encoded in features.
- Retention actions should be proportional to value, not just churn risk.
- High-value customers flagged for retention must be reviewed by humans.

## 8) Monitoring & Retraining
**Monitoring Metrics:**
- Input drift: Feature distributions vs baseline (PSI/KS test).
- Prediction drift: Daily churn-probability histogram.
- Business metrics: Save-rate and campaign ROI by segment.
- API metrics: Request count, latency (p95), error rates.

**Retraining Triggers:**
- Material drift (PSI > 0.25) + precision drop.
- Major product/policy change.
- New cohort with fundamentally different patterns.
- Quarterly evaluation minimum.

## 9) When NOT To Use
- As sole decision-maker for high-impact policies.
- If required input fields are missing or stale.
- During major marketing shifts or campaigns.
- For customers with < 30 days of history.
