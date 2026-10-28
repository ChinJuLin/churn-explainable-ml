# Customer Churn Across Satisfaction Segments: Explainable ML for CRM

*MSc Business Analytics dissertation, University of Bath (2026)*

📄 [Full dissertation (PDF)](report/dissertation_churn_satisfaction_segments.pdf)

## Business question
Satisfied customers still leave and dissatisfied customers often stay. Most churn models treat satisfaction as one predictor among many and produce one averaged explanation. **Do the drivers of churn differ between low-, medium- and highly-satisfied customers, and should retention actions differ too?**

## Data
E-commerce customer dataset ([Kaggle, Verma 2021](https://www.kaggle.com/datasets/ankitverma2010/ecommerce-customer-churn-analysis-and-prediction)): **5,630 customers, 948 churned (16.8%)**.
Satisfaction (1–5) was grouped at the two largest jumps in churn rate: **low (1–2), medium (3–4), high (5)**.

## Method
| Step | What | Why |
|---|---|---|
| Model | XGBoost: one pooled model + one per segment | Strong on tabular data, works with SHAP |
| Validation | Stratified 5-fold CV; ROC-AUC and Average Precision | Churn classes are imbalanced |
| Robustness | Label permutation, preprocessing variants, feature ablation, learning curves, duplicate check | Rule out leakage / inflated scores |
| Explanation | SHAP + 50-sample bootstrap of feature rankings | Compare drivers across segments and check they are stable |
| Profiling | RFM (recency, frequency, monetary) profiles | Give the model output a behavioural meaning for CRM teams |

## Results
- All four models separate churned from retained customers well: **ROC-AUC > 0.97**, Average Precision **0.89–0.98** (vs. baselines of 0.12–0.24).
- **Tenure is the #1 driver in every segment**, with fully stable bootstrap rankings.
- **The #2 driver differs by segment:**

  | Segment | 2nd most important driver | Retention action |
  |---|---|---|
  | Low satisfaction | Cashback amount | Monitor monetary value / incentives |
  | Medium satisfaction | Complaint status | Fast complaint resolution |
  | High satisfaction | Number of registered addresses (and delivery distance) | Review account and delivery experience |

- RFM: customers who **ordered recently but rarely and with low spend** have the highest churn in every segment, a clear early-warning group.

**Takeaway:** segments share a common core (tenure) but weight other signals differently, so CRM should combine one lifecycle strategy with segment-specific diagnosis.

## Honest limitations
Churn is a status recorded in the dataset with undocumented timing, so the high scores show separability in this data, not proven forward-looking accuracy. Recommendations are framed as hypotheses to test prospectively.

**Tools:** Python, pandas, scikit-learn, XGBoost, SHAP, SciPy, matplotlib, seaborn
