# Day 3 - Titanic Logistic Regression (CV + ROC)

Artifacts:
- 'titanic_cv_results.md' - 5-fold CV (Accuracy, F1, ROC-AUC)
- 'titanic_roc_curve.png' - ROC curve on holdout test

Notes:
- Used 'class_weight="balanced"' for class imbalance.
- Cross-validation with 'StratifiedKfolds(n_splits=5)'.
- Features: sex, age, fare, class, embarked, sibsp, parch, alone.
