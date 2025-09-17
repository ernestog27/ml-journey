# Day 5 – Credit Card Fraud Detection (Imbalanced Data)

## Overview

This project tackles the **Kaggle Credit Card Fraud Detection dataset** (~285k transactions, only 0.17% fraud).  

The challenge: class imbalance makes accuracy meaningless: a model predicting "non-fraud" always would score ~99% accuracy but detect **zero frauds**.

Fraud detection (like cybersecurity intrusion detection) requires focusing on **recall and precision**, not just accuracy.

---

## Models & Methods

- **Baseline models:** Logistic Regression, Random Forest  
- **Evaluation metrics:** Accuracy, Precision, Recall, F1, ROC-AUC, PR-AUC  
- **Imbalance handling:**
  - Class weights (`class_weight="balanced"`)  
  - SMOTE oversampling (via `imblearn.Pipeline`)  
- **Threshold scanning:** Tested thresholds from 0.05 → 0.95 to find the best precision/recall trade-off  

---

## Results Summary

### Baseline Metrics (default threshold = 0.5)

| Model               | Accuracy | Precision | Recall | F1   | ROC-AUC | PR-AUC |
|----------------------|----------|-----------|--------|------|---------|--------|
| Logistic Regression  | 0.998    | 0.80      | 0.62   | 0.70 | 0.95    | 0.70   |
| Random Forest        | 0.999    | 0.92      | 0.60   | 0.73 | 0.97    | 0.74   |

---

### Threshold Tuning (Logistic Regression, class_weight="balanced")

Scanning thresholds from 0.50 → 0.95 showed that as we raise the threshold, **precision increases** while recall stays consistently hig
  
The model is able to catch nearly ~89% of fraud cases even at very strict thresholds.

| Threshold | Precision | Recall | F1   |
|-----------|-----------|--------|------|
| 0.50      | 0.058     | 0.918  | 0.109 |
| 0.75      | 0.122     | 0.898  | 0.214 |
| 0.90      | 0.192     | 0.888  | 0.315 |
| 0.95      | 0.269     | 0.888  |412 |

👉 **Best trade-off (
by F1):**  
- Threshold ≈ **0.95** → Recall = **0.888**, Precision = **0.269**, F1 = **0.412**

---

#
## Interpretation
- At lower thresholds (e.g., 0.50), recall is very high (~0.92) but precision is extremely low (~0.06), meaning 
ny false alarms.  
- At higher thresholds (e.g., 0.95), precision improves (~0.27) while recall remai
ns high (~0.89).  
- The best F1 (0.41) occurs at threshold = **0.95**, suggesting this dataset favors a very conservative cutoff when balancing precision arecall.

---

## 📊 Key Plots
- ROC Curve (baseline vs balanced)  
- Precision-Recall Curve (focion/Recall/F1 plot  

Exa(cc_imbalanced_day_05_roc_baselines.png) ard_roc_curv(cc_imbalanced_day_05_PR_curves_baselines.png) chreshold_s.png)  


---

## 📝 Takeaways
- Fraud detection requi:s **recall focus** — catching more frauds matters even with more false positives.  
- Class weighting and SMOTE both improved recall compared to naive baselines.  
- **Threshold scanning** allowed balancing precision vs recall to match business costs.  
- In real deployment, the choice of threshold depends on the trade-off between customer friction (false positives) and financial loss (false negatives).

---

## 📂 Artifacts
- [Notebook](../notebooks/05_creditcard_imbalanced.ipynb)  
- Plots saved under `docs/`  
- Metrics & threshold results documented here