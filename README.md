# Telco Customer Churn — Model Monitoring Project

Course group project: classify customer churn using the [Telco Customer Churn dataset](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) and build toward a simulated live monitoring dashboard.

## Current milestone: working baseline

- **Baseline:** Decision Tree classifier
- **Comparison:** Random Forest classifier (200 trees)
- **Data split:** stratified 80% training / 20% held-out test, `random_state=42`
- **Preprocessing:** convert `TotalCharges` to numeric; set 11 blank entries with zero tenure to zero; exclude `customerID` from modeling; encode categorical features with a training-fitted `OneHotEncoder` in a scikit-learn pipeline
- **Primary metrics:** recall and F1-score for churn (`Churn=1`)
- **Supporting metrics:** ROC-AUC, precision and accuracy

### Baseline results (held-out test set)

| Metric | Decision Tree | Random Forest |
| --- | ---: | ---: |
| Accuracy | 0.7168 | 0.7850 |
| Precision (churn) | 0.4675 | 0.6203 |
| Recall (churn) | 0.4813 | 0.4893 |
| F1-score (churn) | 0.4743 | 0.5471 |
| ROC-AUC | 0.6414 | 0.8200 |

The majority-class (always predict no churn) accuracy is 0.7346. These reported metrics are from the team's executed baseline notebook, not from the monitoring dashboard. Scores could differ if dependencies or model settings change.

## Repository structure

```text
telco-churn-monitoring/
├── README.md                       # Project overview and actual baseline results
├── requirements.txt                # Python dependencies
├── .gitignore                      # Ignore downloaded datasets and local files
├── data/
│   └── README.md                   # Kaggle source and download instructions
└── notebooks/
    └── baseline_model.ipynb       # Baseline training and evaluation
```

## How to run locally

1. Clone or download this repository.
2. Download the dataset, following [data/README.md](data/README.md).
3. From the repository root, create a virtual environment and install dependencies:

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   jupyter notebook notebooks/baseline_model.ipynb
   ```

4. In the notebook, choose **Run All**. The existing stored outputs show the original executed metrics.

## Google Colab

Upload `notebooks/baseline_model.ipynb` to [Google Colab](https://colab.research.google.com/), then upload `WA_Fn-UseC_-Telco-Customer-Churn.csv` using the Colab Files panel. Select **Runtime → Run all**. Colab normally includes the core ML dependencies. Uploaded files may need to be uploaded again after a runtime reset.

## Evaluation choices

Recall is a primary metric because missed churners represent lost chances to intervene. F1-score balances recall against wasted retention outreach to customers who would stay. ROC-AUC measures discrimination across thresholds, while accuracy alone is misleading with an approximately 26.54% churn rate.

## Project scope and next steps

The baseline uses a static sample, not a true incoming stream. Planned later work: simulate input batches, log predictions, track input and prediction-distribution changes, and display performance in Streamlit. Any relabeling-based concept drift demonstration will be identified as synthetic. Decision Trees and Random Forests do not update automatically after training.

## Group contributions

Each group member should make **their own commit using their own GitHub account** so the repository's commit history demonstrates participation. Assign actual names/roles in the project submission or task matrix; do not claim commits before they're made.
