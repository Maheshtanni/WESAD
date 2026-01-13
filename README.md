# Wrist vs Chest Stress Detection (WESAD) — LOSO Evaluation

## Overview
This project tests whether **wrist-worn physiological signals** can outperform **chest-mounted sensors** for stress detection under **strict subject-independent evaluation**.

Most prior results are inflated by subject-dependent splits. Here, both wrist and chest models are evaluated using **Leave-One-Subject-Out (LOSO) cross-validation**, where the test subject is completely unseen during training.

---

## Problem
Chest sensors (ECG/Resp/EDA) are often assumed to be superior because they measure physiology directly. But under **real-world constraints**, models must generalize to **new users**, and performance often collapses when evaluated properly (LOSO). This project re-checks that assumption using a fair, reproducible protocol.

---

## Dataset
- **WESAD** dataset (15 subjects)
- **Task:** Binary classification → Stress vs Non-Stress  
- **Wrist signals:** BVP, ACC, TEMP  
- **Chest signals:** ECG, Resp, EDA, Temp  

> Note: WESAD is not included in this repo. Download it and place it as described below.

---

## Method
- **Protocol:** Leave-One-Subject-Out (LOSO)
- **Model:** XGBoost
- **Preprocessing:** filtering + windowing + physiological feature extraction
- **Imbalance handling:** SMOTE applied to **training data only**
- **Metrics:** F1, Precision, Recall, ROC-AUC + aggregated confusion matrix
- **Statistics:** Wilcoxon signed-rank test + rank-biserial effect size
- **Interpretability:** SHAP feature importance (trained on full dataset for global explanations)

---

## Key Results (Summary)
- Wrist model achieves higher mean F1 than chest baseline under LOSO
- Improvement is statistically significant (Wilcoxon p < 0.05)
- High recall (~0.96) and strong ROC-AUC (~0.96)
- SHAP indicates multimodal contributions (cardiovascular + motion + temperature)

(See `figures/` for plots.)

---

## Repository Structure
