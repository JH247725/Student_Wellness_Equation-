[README.md](https://github.com/user-attachments/files/33683625/README.md)
# The Student Wellness Equation

An interactive Streamlit dashboard for the Student Health Risk tabular machine-learning project.

## Research question

Can lifestyle habits—study hours, sleep hours, screen time, stress level, diet quality, and exercise hours—help predict a student's `Health_Risk` category (Low, Medium, or High)?

## Dashboard features

- Overview of the labeled dataset and health-risk distribution
- Interactive lifestyle comparisons with Plotly
- Model performance metrics from the executed notebook's stratified 80/20 validation split
- Permutation feature importance
- A prediction demo powered by a saved Random Forest pipeline

> **Important:** This is an educational project, not a medical tool. Predictions are not diagnoses. Predictive importance and associations do not establish causation.

## Repository structure

```text
.
├── app.py
├── requirements.txt
├── README.md
└── tabular/
    ├── data/
    │   ├── train.csv
    │   └── test.csv
    ├── models/
    │   └── health_risk_model.joblib
    ├── notebooks/
    │   └── health_risk_project.ipynb
    ├── outputs/
    │   ├── feature_importance.csv
    │   ├── model_metrics.json
    │   └── test_predictions.csv
    └── src/
        └── train_model.py
```

## Dataset

The supplied training data contains 4,000 labeled records; the supplied test data contains 1,000 records without target labels. The six model predictors are:

- Numeric: `Study_Hours`, `Sleep_Hours`, `Screen_Time`, `Exercise_Hours`
- Categorical: `Stress_Level`, `Diet_Quality`

The `id` column is excluded from model features.

Training target distribution:
- Low: 65.25%
- Medium: 26.60%
- High: 8.15%

## Model and validation

The notebook's selected model is a tuned Random Forest with a preprocessing pipeline (StandardScaler for numeric columns and OneHotEncoder for categorical columns). The tuned settings recorded in the notebook are:

- `n_estimators=100`
- `max_depth=10`
- `min_samples_leaf=4`
- `min_samples_split=2`
- `max_features="sqrt"`
- `class_weight="balanced"`
- `random_state=42`

Recorded validation metrics from the notebook's stratified 80/20 split (800 validation records):
- Accuracy: 76.00%
- Balanced accuracy: 74.48%
- Macro F1: 0.7034
- High-risk recall: 81.54%
- High-risk precision: 58.24%

The validation metrics shown by the dashboard are the results recorded in the notebook. The saved prediction pipeline is retrained on all 4,000 labeled records for the interactive demo and should not be used to re-estimate those holdout metrics.

## Run locally

Python 3.11 is recommended.

1. Clone this repository.
2. Create and activate a virtual environment.
3. Install dependencies.
4. Run Streamlit.

```bash
python -m venv .venv
# Windows PowerShell:
.venv\Scripts\Activate.ps1
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
streamlit run app.py
```

## Rebuild the saved model

From the repository root:

```bash
python tabular/src/train_model.py
```

This fits the specified Random Forest pipeline on the labeled training data and writes the model to `tabular/models/health_risk_model.joblib`. It does not reproduce the notebook's hyperparameter search; the tuned parameters are specified from the notebook's recorded best result.

## Deploy on Streamlit Community Cloud

1. Push this repository to GitHub.
2. Open https://share.streamlit.io/ and sign in with GitHub.
3. Choose this repository, branch `main`, and main file path `app.py`.
4. Deploy and wait for the build to complete.
5. Open the app URL and test each tab.

## Reproducibility checklist

- Execute the notebook from top to bottom and save outputs before submitting.
- Confirm `train.csv` and `test.csv` paths work from a fresh clone.
- Keep `requirements.txt` up to date.
- Verify that the GitHub repository does not contain secrets or data you are not permitted to share.
- Do not claim that test predictions are validated: the test CSV has no ground-truth `Health_Risk` labels.
