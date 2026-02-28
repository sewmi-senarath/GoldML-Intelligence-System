# GoldML Intelligence System

## Project Overview
The **GoldML Intelligence System** is a supervised machine learning project for **gold market analysis and prediction** using historical gold price data. The project focuses on four independent but related analytical components that support practical financial decisions:

1. Gold price forecasting (regression)
2. Next-day market trend prediction (binary classification)
3. Volatility-based risk classification (multi-class classification)
4. Investment decision support (Buy / Hold / Sell classification)

This repository is structured for collaborative implementation, where each team member develops their assigned component separately and all components are integrated into one final system.

---

## Dataset
- **Source:** Kaggle
- **Dataset Link:** https://www.kaggle.com/datasets/ayeshaseherr/gold-prise
- **Dataset Name:** Gold Market Analysis – 10 Years of Data
- **Kaggle Reference:** `ayeshaseherr/gold-prise`
- **Subtitle (Kaggle):** An in-depth analysis of market trends, volatility, and price movements from 2016
- **License:** CC0: Public Domain
- **Last Updated (Kaggle):** 2026-02-21

### Data Scope and Usage
- Use the exact dataset version from the Kaggle link above for all components.
- Features used in modeling must come from available dataset columns and clearly documented derived features.
- If any feature is engineered (e.g., rolling indicators, lag values, momentum fields), document the formula and window size in the component notebook.

> [!NOTE] 
> Team members should use the same dataset version and document any preprocessing assumptions to maintain consistency across components.

> [!IMPORTANT]
> The project plan specifies **no structural dataset modification**. Only preprocessing and feature engineering are allowed.

---

## Project Objectives
1. Forecast next-day gold closing price using regression.
2. Predict whether market direction is up or down for short-term decisions.
3. Classify market risk using volatility behavior.
4. Generate actionable investment signals: **Buy / Hold / Sell**.
5. Deliver a reproducible and interpretable machine learning workflow.

---

## Team Component Allocation (Mandatory Separate Implementation)
Each member must complete their assigned component independently, with separate notebooks/scripts before final integration.

| Member | Component | Task Scope | Deliverable |
|---|---|---|---|
| Member 1 | Price Prediction | Regression pipeline, lag feature generation, model training/evaluation | `price_prediction.ipynb` + metrics summary |
| Member 2 | Trend Classification | Binary label generation (UP/DOWN), classification training/evaluation | `trend_classification.ipynb` + classification report |
| Member 3 | Risk Classification | Risk labeling using volatility thresholds, multi-class modeling | `risk_classification.ipynb` + confusion matrix |
| Member 4 | Investment Signal | Buy/Hold/Sell label strategy, feature engineering, final classifier | `investment_signal.ipynb` + decision output summary |

> Replace placeholders with actual student names and IDs in the final submission.

---

## Planned ML Components

### Price Prediction (Regression)
- **Objective:** Predict next-day `Close` price
- **Inputs:** `Open`, `High`, `Low`, `Close`, `Volume`, lag features such as `Close(t-1)`, `Close(t-2)`
- **Target:** Next-day close price
- **Planned Models:** Linear Regression, Random Forest Regressor
- **Metrics:** RMSE, R²

### Trend Classification (UP/DOWN)
- **Objective:** Predict whether tomorrow’s price increases or decreases
- **Inputs:** `Open`, `High`, `Low`, `Close`, `Volume`, `Daily_Return`
- **Target:** Binary label (1 = UP, 0 = DOWN), based on `Close(t+1)` vs `Close(t)`
- **Planned Models:** Logistic Regression, SVM
- **Metrics:** Accuracy, Precision, Recall, F1-score

### Risk Classification (Volatility-Based)
- **Objective:** Classify risk as Low / Medium / High
- **Inputs:** `Daily_Return`, `Volatility_20`, `Volume`
- **Target:** Multi-class risk label from volatility thresholds
- **Planned Models:** Decision Tree Classifier, K-Nearest Neighbors (KNN)
- **Metrics:** Accuracy, Confusion Matrix

### Investment Signal (BUY/HOLD/SELL)
- **Objective:** Generate practical daily gold investment signal
- **Inputs (planned):** momentum, trend, risk, and volume features (e.g., 7-day return, 30-day return, `MA_20-MA_50`, `MA_50-MA_200`, `Volatility_20`, volume percentage change)
- **Target:** Multi-class decision label (2 = BUY, 1 = HOLD, 0 = SELL)
- **Planned Models:** Gradient Boosting Classifier, K-Nearest Neighbors (KNN)
- **Metrics:** Accuracy, Precision, Recall, Confusion Matrix

---

## Recommended Repository Structure
```
GoldML-Intelligence-System/
├─ data/
│  ├─ raw/
│  │  └─ Gold_Market_10y.csv
│  └─ processed/
│     └─ shared_features.csv
├─ notebooks/
│  ├─ price_prediction.ipynb
│  ├─ trend_classification.ipynb
│  ├─ risk_classification.ipynb
│  ├─ investment_signal.ipynb
│  └─ integration_summary.ipynb
├─ outputs/
│  ├─ price_prediction/
│  ├─ trend_classification/
│  ├─ risk_classification/
│  └─ investment_signal/
├─ src/
│  ├─ price_prediction/
│  ├─ trend_classification/
│  ├─ risk_classification/
│  └─ investment_signal/
├─ reports/
│  ├─ member_contributions.md
│  └─ final_report.pdf
├─ requirements.txt
└─ README.md
```

> [!NOTE]
> Keep it simple: one main notebook per component, one output folder per component.

> [!IMPORTANT]
> `.gitkeep` files are folder placeholders only. They are **not** expected project outputs.
> Expected outputs are the files shown above (for example, `price_prediction.ipynb`, `shared_features.csv`, and `final_report.pdf`).

---

## Suggested Tech Stack
- **Language:** Python 3.10+
- **Core Libraries:** pandas, numpy, matplotlib, seaborn, scikit-learn
- **Optional:** xgboost/lightgbm, statsmodels, jupyter
- **Version Control:** Git + GitHub

---

## Setup Instructions
1. Clone the repository:
   ```bash
   git clone https://github.com/JordanCJ7/GoldML-Intelligence-System.git
   cd GoldML-Intelligence-System
   ```
2. Create and activate a virtual environment.
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Download the dataset from Kaggle and place it in `data/raw/` as `Gold_Market_10y.csv`.
5. Run notebooks/scripts according to assigned component.

### First Data Check (All Members)
Before starting your component, verify you can load the same file:

```python
from pathlib import Path
import pandas as pd

data_path = Path("data/raw/Gold_Market_10y.csv")
assert data_path.exists(), f"Dataset not found: {data_path}"

df = pd.read_csv(data_path)
print(df.shape)
print(df.columns.tolist())
```

---

## Workflow and Integration Guidelines
- Each member works only on their assigned component files.
- Use one branch per member: `member-<id>-<module-name>`.
- Minimum files per member:
   - one notebook in `notebooks/`
   - optional helper code in `src/<module-name>/`
   - metrics/results in `outputs/<module-name>/`
- Do not overwrite other members’ component folders.
- After all 4 components are complete, create `notebooks/integration_summary.ipynb` to compare results and finalize conclusions.
- Keep preprocessing and label logic documented in the component notebook.

---

## Evaluation Criteria (Project Quality Focus)
The final integrated submission should demonstrate:
- Correct and clean data processing pipeline
- Strong exploratory analysis with meaningful insights
- Appropriate feature engineering decisions
- Well-justified model selection and tuning
- Clear metric-based performance comparison
- Professional presentation of findings and recommendations

---

## Deliverables
1. Four separate component notebooks/scripts (one per member)
2. Shared preprocessing notes and feature definitions
3. Model outputs and metrics for each component
4. Final integrated system summary
5. Evaluation tables and confusion matrices
6. Final report/presentation assets and updated documentation

---

## Academic and Professional Standards
- Keep all work original and properly attributed.
- Do not copy code or reports without citation.
- Ensure all charts, metrics, and claims are reproducible.
- Use clear commit messages and maintain traceable contribution history.

---

## Maintainers
- **Team:** GoldML Intelligence System Group
- **Institution/Course:** Sri Lanka Institute of Information Technology (SLIIT) - Machine Learning
- **Course Code:** IT4060
- **Semester/Year:** Year 4 Semester 1, 2026

---

## Quick Customization Checklist
Before final submission, update the following in this README:
- [ ] Team member names and student IDs
- [ ] Exact model list used in implementation
- [ ] Final performance metrics
- [ ] Repository URL and branch strategy
- [ ] Course code, module title, lecturer details
- [ ] Add/create `requirements.txt`
- [ ] Replace scaffold placeholders with actual notebooks, outputs, and report files