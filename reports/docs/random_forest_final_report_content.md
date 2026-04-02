# Random Forest Final Report Content

## Purpose
This document gives you the final report content and the exact narrative you should use for the Random Forest component. It is written to help you maximize marks by making the methodology clear, the evaluation honest, and the discussion strong.

## What To Emphasize For Top Marks
1. Use a leakage-safe time-series workflow.
2. Explain why you predicted price change first and reconstructed the next-day close.
3. Show that you engineered meaningful technical features, not just raw OHLC data.
4. Report the held-out test results clearly, not only the training results.
5. Discuss the trade-off between accuracy, stability, and interpretability.
6. Be honest that another model may be slightly better on some metrics, but Random Forest remains strong because it is robust and explainable.

## Paste-Ready Report Draft

### 1. Project Title
Gold Price Prediction Using Random Forest Regressor

### 2. Problem Statement
The objective of this project is to predict the next trading day gold closing price using historical market data and engineered technical indicators. Since financial prices are time-dependent and non-stationary, a standard random train-test split would create leakage and lead to overly optimistic results. For that reason, the solution uses a chronological split and time-series aware cross-validation.

### 3. Dataset Overview
The dataset contains 10 years of daily gold market data, including Date, Close, Open, High, Low, Volume, and several precomputed technical fields such as Daily_Return, moving averages, and volatility. The records were sorted chronologically before modeling so that all transformations respect time order.

### 4. Data Cleaning
Rows with missing values caused by rolling calculations were removed before model training. This is important because filling rolling-window gaps with artificial values can distort momentum and volatility patterns. After cleaning, the dataset was ready for feature engineering with no remaining missing values in the modeling frame.

### 5. Feature Engineering
To capture both short-term and medium-term market behavior, the following feature groups were created:
- Lag features: Close_lag_1, Close_lag_2, Close_lag_3, Close_lag_5
- Return features: Return_1d, Return_2d, Return_5d, Return_10d
- Momentum indicators: RSI_14, MACD, MACD_signal, MACD_hist
- Volatility features: BB_width, Volatility_20
- Intraday structure: HL_spread_pct, OC_change_pct
- Liquidity change: Volume_change
- Relative level features: Dist_MA20_pct, Dist_MA50_pct, Dist_MA200_pct
- Calendar fields: Year, Month, Day_of_Week, Quarter

These features are valuable because gold price movement is influenced by trend strength, recent momentum, volatility expansion, and relative deviation from moving averages.

### 6. Modeling Strategy
Instead of predicting the absolute next-day close directly, the model predicts the daily price change:

Predicted_Change = Close_tomorrow - Close_today

The final close prediction is then reconstructed as:

Predicted_Tomorrow_Close = Today_Close + Predicted_Change

This approach is stronger for tree-based models because it focuses the learning task on local movement rather than the long-run price level. It also makes the model more stable when the market shifts upward over time.

### 7. Train-Test Design
The dataset was split chronologically using an 80/20 split so that the model was trained only on earlier observations and evaluated on later unseen data. Hyperparameter tuning used GridSearchCV with TimeSeriesSplit, which preserves time order inside the validation folds. This prevents leakage and gives a more realistic estimate of generalization.

### 8. Hyperparameter Tuning
The best model found by GridSearchCV used the following parameters:
- n_estimators: 400
- max_depth: 12
- min_samples_split: 10
- min_samples_leaf: 2
- max_features: sqrt

This configuration balances model flexibility with regularization. It is deep enough to capture non-linear relationships, but constrained enough to reduce overfitting.

### 9. Final Random Forest Results
The final Random Forest model achieved the following held-out test results on reconstructed absolute price:
- Test R2: 0.995997
- Test MAE: 2.6982
- Test RMSE: 3.8228
- Test MAPE: 0.9203%
- OOB score: -0.042801

The negative OOB score should not be treated as the main conclusion. In financial time series, OOB can be unstable because the distribution drifts over time. The held-out chronological test metrics are the correct metrics to prioritize in the report.

### 10. Interpretation Of Results
The model shows strong level-tracking on the test set, with predictions closely following the actual close price trajectory. The scatter plot should sit near the diagonal, which indicates limited systematic bias. Residuals remain centered around zero, although some larger errors appear when the market moves sharply.

The feature-importance output shows that the model relies most on technical structure and momentum signals. The strongest features include BB_width, OC_change_pct, MACD_signal, Return_2d, Return_10d, Dist_MA200_pct, Return_5d, Volume, MACD, Dist_MA50_pct, HL_spread_pct, MACD_hist, Volatility_20, Dist_MA20_pct, and Volume_change. This supports the idea that the model is learning both trend continuation and short-term volatility regime changes.

### 11. Cross-Model Comparison
Use the following final comparison table in your report:

| Model | Test R2 | Test MAE | Test RMSE |
| --- | ---: | ---: | ---: |
| Linear Regression | 0.996419 | 2.604220 | 3.751325 |
| Gradient Boosting | 0.996318 | 2.587100 | 3.666500 |
| Random Forest | 0.995997 | 2.698227 | 3.822797 |
| SVR | 0.997079 | 0.667285 | 3.518468 |

### 12. Ranking Discussion
If you rank models by the average of R2, MAE, and RMSE, SVR comes first, followed by Gradient Boosting, then Linear Regression, and finally Random Forest. You should not hide this. Instead, explain the Random Forest choice using engineering and presentation value:
- It is leakage-safe.
- It is stable and robust.
- It handles non-linear interactions well.
- It provides direct feature importance.
- It is easy to explain during viva.

This is a stronger report strategy than pretending it is the best on every metric.

### 13. Why Random Forest Is Still A Strong Choice
Random Forest remains a strong final model because it combines robustness, interpretability, and practical reliability. Even when another model gives slightly better raw test metrics, Random Forest still offers a convincing balance between predictive quality and explainability. For an academic project, that balance is often rewarded because it demonstrates methodological maturity rather than only metric chasing.

### 14. Limitations
A strong report should acknowledge the following limitations:
- The model predicts only the next-day close, not intraday extremes.
- A single chronological split does not capture all possible market regimes.
- OOB score is not reliable enough to override the held-out test results in a drifting financial series.
- The model does not yet use walk-forward backtesting or SHAP analysis.

### 15. Future Work
If you want to show excellence, mention these realistic improvements:
- Walk-forward validation with rolling retraining.
- SHAP-based interpretation for feature impact.
- Regime-specific models for low-volatility and high-volatility periods.
- Baseline comparison against naive tomorrow equals today forecasting.
- Feature selection or dimensionality reduction to test whether simpler feature sets can match performance.

### 16. Conclusion
The Random Forest component successfully implements a leakage-safe time-series prediction pipeline for gold prices. The model uses engineered lag, momentum, volatility, and distance-based features to predict next-day movement and reconstruct absolute price. The held-out test results are strong, the feature interpretation is meaningful, and the approach is well suited for an academic financial forecasting report.

## What You Should Say In Your Viva
1. Why did you predict change first instead of absolute price?
2. Why did you use TimeSeriesSplit instead of normal cross-validation?
3. Why is OOB score not the main metric here?
4. Which features mattered most and why?
5. If another model scores better, why keep Random Forest in the report?
6. What would you improve if given more time?

## Member Contribution Text For Random Forest
Use this in member contributions if you need a complete entry:

- **Name:** [Insert Name]
- **ID:** [Insert ID]
- **Branch:** `member-2-random-forest`
- **Notebook:** `notebooks/random_forest/random_forest_gold_prediction.ipynb`
- **Algorithm Justification:** Selected to reduce variance, handle non-linear relationships, and provide a robust ensemble baseline with direct feature-importance interpretation.
- **Summary of work:** Implemented a leakage-safe Random Forest pipeline with lag, momentum, volatility, and moving-average-distance features, tuned hyperparameters using GridSearchCV with TimeSeriesSplit, reconstructed next-day absolute prices from predicted change, evaluated performance using MAE, RMSE, R2, and MAPE, and exported predictions and feature importance for the final report.

## Final Advice
Do not frame Random Forest as the best model by raw metrics if the comparison table says otherwise. Frame it as the most reliable and explainable ensemble choice for your own component, supported by a careful time-series workflow and clear feature analysis. That is the safest path to a strong mark.
