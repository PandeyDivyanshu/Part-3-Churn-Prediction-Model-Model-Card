# Error Analysis
Model: Gradient Boosting (threshold=0.4)
Test set size: 336
Total FP: 49
Total FN: 22

## False Positives (Predicted Churn but Actually Retained)

Business risk: Unnecessary retention spend / potential margin leakage.

| Customer ID | Model Prob | Recency | Frequency | Spend | Tickets | Return % | Sessions | Reason |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| CUST00437 | 0.972 | 151d | 1 | ₹729 | 0 | 0.0% | 0 | High engagement but low spend |
| CUST01370 | 0.956 | 161d | 2 | ₹1246 | 0 | 0.0% | 2 | High engagement but low spend |
| CUST01246 | 0.955 | 262d | 0 | ₹0 | 0 | 0.0% | 1 | High engagement but low spend |
| CUST01614 | 0.948 | 103d | 2 | ₹1352 | 0 | 50.0% | 4 | Recently engaged but had not purchased |
| CUST01017 | 0.946 | 133d | 2 | ₹1167 | 0 | 50.0% | 3 | Recently engaged but had not purchased |
| CUST00491 | 0.939 | 97d | 1 | ₹541 | 1 | 100.0% | 10 | Recently engaged but had not purchased |

## False Negatives (Predicted Retention but Actually Churned)

Business risk: Missed save opportunity and potential LTV loss.

| Customer ID | Model Prob | Recency | Frequency | Spend | Tickets | Return % | Sessions | Reason |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| CUST00088 | 0.379 | 98d | 2 | ₹1169 | 0 | 0.0% | 9 | Price-sensitive customer lost to competitor |
| CUST00379 | 0.367 | 75d | 1 | ₹538 | 0 | 0.0% | 2 | Sudden activity drop not captured strongly |
| CUST00438 | 0.364 | 64d | 3 | ₹2466 | 2 | 100.0% | 6 | Return behavior trending but not flagged |
| CUST01028 | 0.348 | 173d | 1 | ₹2810 | 0 | 0.0% | 6 | Sudden activity drop not captured strongly |
| CUST00397 | 0.310 | 79d | 1 | ₹1203 | 1 | 0.0% | 3 | Sudden activity drop not captured strongly |
| CUST02103 | 0.282 | 44d | 2 | ₹1052 | 1 | 0.0% | 0 | Very low engagement despite moderate spend |

## Recommendations

### To Reduce False Positives:
- Add recent engagement/recency trend feature (trending up = lower churn)
- Consider return/refund patterns as negative signal
- Lower importance of single high-value transactions

### To Reduce False Negatives:
- Add recency velocity (rate of change in days since last purchase)
- Track category switching patterns
- Incorporate competitor mention/survey data if available
- Add seasonal cohort effects
