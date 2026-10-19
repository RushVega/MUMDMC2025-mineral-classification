# Results exported for GitHub review

These compact tables were copied or transcribed from **saved output cells in the final submitted notebook**. They are provided so reviewers can inspect the reported metrics without retraining heavy CNN models. The values are **rounded to three decimal places**, not raw-precision log files.

| File | Contents |
| --- | --- |
| `baseline_models.csv` | DT/KNN evaluation at 224×224 and 150×150 |
| `cv_fold_results.csv` | Experiment 2: each of 5 folds per model |
| `cv_summary.csv` | Experiment 2: mean and standard deviation |
| `tuning_grid.csv` | Experiment 3: nine hyperparameter candidates |
| `tuned_test.csv` | Experiment 3: selected models' holdout evaluation |
| `cnn_metrics.csv` | Experiment 5: head-only and fine-tuned CNN scores |

Macro-F1 and weighted F1 are different measures; when metrics are compared with paper Table 3, verify how that table defines averaging. The paper's 2,500-image results and this project's 583-image results are **not directly matched test sets**. No CSV is presented as a new independent run.

More detailed logs, per-class classification reports, confusion matrices and training histories are preserved in the notebook outputs and generated on a fresh Colab run.
