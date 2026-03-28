# Model Selection and Hyperparameter Tuning Report

## Candidate Models Evaluated

Each model was evaluated with 5-fold stratified cross-validation on the
training set. Results are sorted by mean weighted F1 score.

| Model | Mean CV Accuracy | Mean Weighted F1 | Training Time (s) |
|-------|-----------------|------------------|-------------------|
| LightGBM | 0.6133 | 0.5983 | 15.5 |
| Random Forest | 0.5994 | 0.5754 | 9.6 |
| MLP | 0.5775 | 0.5569 | 4.5 |
| Logistic Regression | 0.5647 | 0.5358 | 1.2 |
| SVM | 0.5594 | 0.5209 | 5.5 |
| KNN | 0.5419 | 0.5199 | 1.9 |

## Selected Model: LightGBM

**LightGBM** was selected based on the highest mean weighted F1 score.

### Selection Rationale

- **LightGBM** achieved the best balance of accuracy and F1 across
  all five folds, indicating strong generalisation.
- It handles the 114-class problem efficiently through gradient boosting on
  decision trees, which naturally captures non-linear feature interactions.
- Training time is competitive given the dataset size.

### Why Others Were Not Selected

- **Random Forest** (F1=0.5754): Lower weighted F1 than the selected model.
- **MLP** (F1=0.5569): Lower weighted F1 than the selected model.
- **Logistic Regression** (F1=0.5358): Lower weighted F1 than the selected model.
- **SVM** (F1=0.5209): Lower weighted F1 than the selected model.
- **KNN** (F1=0.5199): Lower weighted F1 than the selected model.

## Hyperparameter Tuning

Optuna was used with the TPE sampler for 50 trials.
The search used 3-fold stratified CV as the inner objective.

- Baseline weighted F1 (default params): **0.5983**
- Tuned weighted F1 (best trial):        **0.6046**
- Improvement: **+0.0063**

### Best Hyperparameters Found

| Parameter | Value |
|-----------|-------|
| n_estimators | 443 |
| learning_rate | 0.029615301618026106 |
| num_leaves | 121 |
| max_depth | 9 |
| min_child_samples | 58 |
| subsample | 0.9795081755652144 |
| colsample_bytree | 0.9077713024300027 |
| reg_alpha | 0.000408386047308235 |
| reg_lambda | 0.00441143422327024 |