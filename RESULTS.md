# Real-data evaluation — 2026-11-02

Input: `Spam/SPAM text message 20170820 - Data.csv`. Dataset SHA-256: `1f0573aa3e3e8f5b37a753a454058a9ef9ebb981bcabeeb7ef43cdccedaecf29`.

Model selection used only training-fold CV. One final holdout was reserved before preprocessing. The full CV leaderboard, dependency versions, seed, feature schema and split sizes are in [experiments/report.json](experiments/report.json).

- Model: **ComplementNB**
- Training rows: **4431**; holdout rows: **1141**
- Selection metric: `f1_macro`; selected CV score: **0.962439**
- Dummy baseline CV score on the same folds: **0.463751**
- Five CV folds; seed 42; tuning: **True**
- Identical raw predictor rows grouped: **True**

| Metric | Holdout value |
|---|---:|
| accuracy | 0.979842 |
| balanced_accuracy | 0.959670 |
| f1_macro | 0.955739 |
| roc_auc | 0.990637 |
| average_precision | 0.973676 |

Accuracy 95% Wilson interval: [0.9699, 0.9865]. This treats holdout observations as independent; grouped duplicates reduce the effective sample size, so the interval is descriptive rather than a complete uncertainty estimate.


## Dataset-specific interpretation

Identical raw messages are grouped before holdout and GroupKFold; vocabulary/IDF are learned inside each training fold. Positive class is spam. Near-duplicate/paraphrased messages may remain; the split is not an unseen-campaign or chronological benchmark.

## Reproduce

Activate an environment with the project's requirements, change to the repository root, and run:

```cmd
python -m mlproject train --data "D:\data\Spam\SPAM text message 20170820 - Data.csv" --output artifacts --folds 5 --seed 42 --tune
```

Results were obtained with the dependency versions recorded in the JSON report. Different versions can change results slightly. Negative MAE selection scores are higher-is-better. CV scores are selection estimates and optimistic; the holdout is the final internal result. Hyperparameter tuning is enabled on the smaller datasets and diabetes; for credit, soccer, student and churn the default bounded candidate comparison is used. Scores are not directly comparable across datasets or tasks.

Do not tune against the now-observed holdout or claim improvement over the legacy notebooks: leakage, split policies and preprocessing differ. Raw data, row-level predictions and trained pickle artifacts are not included in this evidence commit.
