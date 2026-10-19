# The Student Wellness Equation

## Project Overview

This project explores whether students' lifestyle habits can be used to predict their health-risk categories using machine learning. We focus on six lifestyle factors: study hours, sleep hours, screen time, stress level, diet quality, and exercise hours.

Our goal is to compare machine learning models and identify which lifestyle factors are most useful for predicting health risk.

## Research Question

Can lifestyle habits predict a student's health-risk level (Low, Medium, or High)?

## Dataset

The project uses the Student Health Risk dataset from the Kaggle Playground Series, Season 6, Episode 7.

- **Training dataset:** 4,000 labeled records
- **Test dataset:** 1,000 records without target labels
- **Target variable:** `Health_Risk`
- **Target categories:** Low, Medium, and High

### Features

**Numerical features**
- `Study_Hours`
- `Sleep_Hours`
- `Screen_Time`
- `Exercise_Hours`

**Categorical features**
- `Stress_Level`
- `Diet_Quality`

The `id` column is excluded from the model features.

## Methods

The project notebook includes:

- Data cleaning and exploratory data analysis
- Analysis of health-risk class distribution
- Chi-square tests for categorical features
- One-way ANOVA for numerical features
- Stratified training and validation split
- Feature preprocessing using `StandardScaler` and `OneHotEncoder`
- Comparison of baseline and advanced machine learning models
- Stratified cross-validation and hyperparameter tuning
- Evaluation using accuracy, balanced accuracy, macro F1-score, and high-risk recall
- Permutation feature importance

## Model Results

The tuned Random Forest was selected as the final model in our notebook.

Recorded validation results:

| Metric | Result |
|---|---:|
| Accuracy | 76.00% |
| Balanced accuracy | 74.48% |
| Macro F1-score | 0.7034 |
| High-risk recall | 81.54% |
| High-risk precision | 58.24% |

Stress level and sleep hours were identified as the most influential predictors in the notebook's permutation feature-importance analysis.

The dataset is imbalanced, with 65.25% of records classified as Low risk, 26.60% as Medium risk, and 8.15% as High risk. For this reason, we considered metrics beyond accuracy when comparing models.

## Repository Structure

```text
.
├── README.md
├── requirements.txt
└── tabular/
    ├── README.md
    ├── health_risk_project.ipynb
    ├── train.csv
    └── test.csv
```

## Requirements

The project uses Python and common data science libraries, including:

- pandas
- NumPy
- scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook

See `requirements.txt` for the listed dependencies.

## How to Run

1. Clone or download this repository.
2. Install the required packages:

   ```bash
   pip install -r requirements.txt
   ```

3. Open the notebook in Jupyter Notebook or JupyterLab.
4. Run the notebook cells in order to reproduce the analysis and model evaluation.

## Limitations

The dataset contains fewer High-risk examples than Low-risk examples, which can affect model performance across categories. The model uses only six lifestyle features, and its predictions should not be treated as medical diagnoses.

The results show predictive associations, not causal relationships. The test dataset does not contain `Health_Risk` labels, so its predictions cannot be evaluated against known outcomes.

## Reproducibility

The notebook contains the project's analysis, model development, and evaluation workflow. Before submission, ensure that all notebook cells have been executed successfully and that the saved notebook includes its outputs, plots, and evaluation results.

## Citations for research papers

Zhang, L., Zhao, S., Yang, Z. et al. An artificial intelligence tool to assess the risk of severe mental distress among college students in terms of demographics, eating habits, lifestyles, and sport habits: an externally validated study using machine learning. BMC Psychiatry 24, 581 (2024). https://doi.org/10.1186/s12888-024-06017-2

Laska, M.N., Pasch, K.E., Lust, K. et al. Latent Class Analysis of Lifestyle Characteristics and Health Risk Behaviors among College Youth. Prev Sci 10, 376–386 (2009). https://doi.org/10.1007/s11121-009-0140-2
