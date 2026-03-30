# GoldML Intelligence System

## Project Overview
The **GoldML Intelligence System** is a supervised machine learning project aimed at solving a real-world financial problem: **Helping investors predict future gold prices to make better buying and selling decisions**. 

This group project utilizes four distinct supervised machine learning algorithms to forecast the daily price change of gold. By comparing the accuracy of these different models, the project determines the most robust approach for time-series financial forecasting.

---

## Dataset
- **Source:** Kaggle
- **Dataset Link:** https://www.kaggle.com/datasets/ayeshaseherr/gold-prise
- **Dataset Name:** Gold Market Analysis – 10 Years of Data
- **Kaggle Reference:** `ayeshaseherr/gold-prise`
- **Subtitle (Kaggle):** An in-depth analysis of market trends, volatility, and price movements from 2016
- **License:** CC0: Public Domain

### Data Scope and Usage
- The dataset undergoes rigorous data preprocessing and feature engineering, including the generation of lag features, percentage returns, and technical indicators (RSI, MACD, Bollinger Bands, Moving Averages).
- The target variable is framed as the **daily price change** (Regression) rather than absolute price, ensuring tree-based algorithms do not face extrapolation issues.

---

## Project Objectives
1. **Forecast next-day gold closing price** using regression techniques.
2. Apply **four distinct supervised learning algorithms** to the same preprocessed dataset.
3. Compare and contrast the different algorithms in terms of their accuracy (MAE, MSE, RMSE, R², MAPE).
4. Provide a critical analysis and discussion on model limitations and potential future work.
5. Deliver a reproducible and professional machine learning workflow using Python and Jupyter Notebooks.

---

## Team Component Allocation (4 Distinct Algorithms)
According to the assignment requirements, the team of 4 members implements 4 distinct algorithms. Each member is responsible for training, tuning, and evaluating their respective model.

| Member | Algorithm | Deliverable |
|---|---|---|
| Member 1 | **Gradient Boosting Regressor** | `gradient_boosting_gold_prediction.ipynb` + metrics |
| Member 2 | **Random Forest Regressor** | `random_forest_gold_prediction.ipynb` + metrics |
| Member 3 | **Linear Regression** (Example) | `linear_regression.ipynb` + metrics |
| Member 4 | **Support Vector Regressor** (Example) | `svr.ipynb` + metrics |

> Replace placeholders with actual student names and IDs in the final submission.

---

## Suggested Repository Structure
```
GoldML-Intelligence-System/
├─ data/
│  └─ Gold_Market_10y.csv
├─ notebooks/
│  ├─ gradient_boosting/
│  │  └─ gradient_boosting_gold_prediction.ipynb
│  ├─ random_forest/
│  │  └─ random_forest_gold_prediction.ipynb
│  ├─ linear_regression/
│  │  └─ linear_regression_gold_prediction.ipynb
│  └─ svr/
│     └─ svr_gold_prediction.ipynb
├─ submission/
│  ├─ members.txt
│  ├─ submission.txt (Contains Dataset, GitHub, & YouTube Links)
│  └─ Final_Report.pdf (Includes code as Appendix)
├─ requirements.txt
└─ README.md
```

---

## Tech Stack
- **Language:** Python 3.10+
- **Environment:** Jupyter Notebook
- **Core Libraries:** pandas, numpy, matplotlib, seaborn, scikit-learn
- **Version Control:** Git + GitHub

---

## Assignment Submission Checklist
To ensure full marks as per the grading rubric, the final submission bundle (`ML-assignment.zip`) must contain:
- [ ] `members.txt` (IDs and emails of all 4 members)
- [ ] `submission.txt` containing:
  - [ ] Link to the public dataset (Kaggle/Cloud)
  - [ ] Link to this public GitHub repository (Must contain detailed commit history)
  - [ ] Link to the YouTube video presentation (Max 20 mins, max 4 mins per member)
- [ ] `Final_Report.pdf` containing:
  - [ ] Problem description & Dataset context
  - [ ] Methodology (Background of 4 algorithms used)
  - [ ] Data Preprocessing and Feature Engineering justification
  - [ ] Results, Algorithm Comparison, and Discussion (Future work)
  - [ ] **Source Code included as text in the Appendix (NO screenshots)**

---

## Evaluation Criteria Highlights
- **No Deep Learning models** are used.
- Correct and robust data processing pipeline.
- Well-justified model selection and hyperparameter tuning.
- Clear metric-based performance comparison among the 4 distinct algorithms.

---

## Maintainers
- **Team:** GoldML Intelligence System Group
- **Institution/Course:** Sri Lanka Institute of Information Technology (SLIIT) - Machine Learning
- **Course Code:** IT4060
- **Semester/Year:** Year 4 Semester 1, 2026