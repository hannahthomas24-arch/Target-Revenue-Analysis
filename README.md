# Target Revenue Analysis

A time series regression analysis of Target Corporation's quarterly revenue, built for Chapman Wealth Management as part of an AFM244 case study with QuantFolio Solutions.

## Overview

This project models Target's quarterly revenue (`saleq`) using a linear time trend plus two seasonal dummy variables, in order to explain historical revenue patterns and support an investment evaluation.

## Files

- `Target_Revenue_Analysis.ipynb` — Google Colab notebook containing the full analysis
- `qSales_2024.csv` — quarterly revenue dataset (Compustat-style fields), filtered to Target (`tic == 'TGT'`)

## Methodology

1. **Data exploration** — loaded and visualized Target's quarterly revenue over time to identify underlying patterns (upward trend, recurring seasonal spikes)
2. **Feature engineering**
   - `time` — sequential quarter counter (1, 2, 3, ...) to capture the overall growth trend
   - `holiday_dv` — dummy variable flagging fiscal Q4 (the holiday shopping quarter)
   - `postholiday_dv` — dummy variable flagging fiscal Q1 (the quarter immediately after the holidays)
3. **Train/test split** — sequential 75/25 split (first 75% of quarters as training data, most recent 25% as testing data), preserving chronological order
4. **Model** — OLS regression: `revenue ~ time + holiday_dv + postholiday_dv`
5. **Evaluation** — model fit statistics (R², Adjusted R², p-values) and confidence intervals via `get_prediction().summary_frame()`
6. **Visualization** — actual vs. predicted revenue plotted over time

## Key Results

- **R² = 0.895** — the model explains about 89.5% of the variation in Target's quarterly revenue
- **Time trend**: statistically significant (p < 0.001), revenue grows by an estimated $139M per quarter on average
- **Holiday dummy (Q4)**: statistically significant (p < 0.001), holiday quarters run roughly $4,472M above baseline
- **Post-holiday dummy (Q1)**: not statistically significant (p = 0.518) — no confirmed distinguishable post-holiday effect
- **Limitation**: the model's linear trend increasingly underpredicts revenue in recent years, suggesting Target's actual growth has accelerated beyond what a straight-line trend captures

## Memo

A brief investment-focused memo is included at the end of the notebook, summarizing the business problem, modeling approach, key findings, and considerations relevant to Chapman Wealth Management's investment decision.

## Tools Used

- Python: `pandas`, `numpy`, `matplotlib`, `statsmodels`
- Google Colab

## Author

Hannah Thomas ([hsthomas@uwaterloo.ca](mailto:hsthomas@uwaterloo.ca))
