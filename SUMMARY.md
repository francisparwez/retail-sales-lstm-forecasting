# Project Summary

## 1. Project Overview

**Project title:** Predictive Analytics on Retail Sales: Time Series Forecasting with LSTM

**Dataset:** Kaggle Store Sales – Time Series Forecasting

**Business context:** Historical retail sales forecasting using data from Corporación Favorita in Ecuador.

**Current stage:** Tasks 1–4 completed; Task 5 results visualisation and final repository delivery are in progress.

The project now includes a naive baseline and an LSTM model trained on 30-day sequences to predict next-day sales. Evaluation on the held-out test period showed lower MAE and RMSE for the LSTM than for the baseline.

## 2. Source Dataset Overview

The initial analysis was performed on `train.csv`.

| Attribute                                  |     Result |
| ------------------------------------------ | ---------: |
| Total rows                                 |  3,000,888 |
| Total columns                              |          6 |
| First date                                 | 2013-01-01 |
| Last date                                  | 2017-08-15 |
| Unique observed dates                      |      1,684 |
| Unique stores                              |         54 |
| Product families                           |         33 |
| Missing values in inspected source columns |          0 |

### Source columns

- `id` — row identifier.
- `date` — date of the sales observation.
- `store_nbr` — store identifier.
- `family` — product family.
- `sales` — sales value.
- `onpromotion` — promotion count as represented in the dataset.

## 3. Descriptive Sales Statistics

| Statistic            |                 Result |
| -------------------- | ---------------------: |
| Total sales          |       1,073,644,952.20 |
| Mean sales per row   |                 357.78 |
| Median sales per row |                  11.00 |
| Minimum sales        |                   0.00 |
| Maximum sales        |             124,717.00 |
| Standard deviation   | Approximately 1,102.00 |

The row-level sales distribution is strongly right-skewed. High values should be investigated in context rather than automatically removed.

## 4. Key EDA Findings

### Sales distribution

The mean is substantially higher than the median, indicating a right-skewed distribution.

### Daily trend and weekly patterns

Aggregated daily sales fluctuate and show an overall upward pattern. The initial weekday comparison showed relatively high sales on Saturday and Sunday, with Thursday lower in that analysis.

### Store and product-family performance

Store 44 led the top-store comparison by cumulative sales. GROCERY I, BEVERAGES, and PRODUCE were the leading product families by cumulative sales in the initial analysis.

### Holiday/event comparison

The preliminary comparison reported average daily sales of approximately 694,431 on dates marked as holidays/events and 627,548 on other dates. This is a descriptive association and does not establish causation.

## 5. Task 2 — Data Preprocessing

### Work completed

- Converted `date` to datetime.
- Checked data types, missing values, exact duplicate rows, and date coverage.
- Aggregated sales across all stores and product families into a daily total.
- Compared observed dates with a complete daily calendar.
- Identified four missing dates: 25 December 2013, 2014, 2015, and 2016.
- Matched these dates to Christmas Day entries in `holidays_events.csv`.
- Created a continuous daily series from 2013-01-01 through 2017-08-15.
- Validated the prepared series.
- Plotted the daily series.
- Saved and reloaded the CSV to verify its contents.

### Prepared dataset

**File:** `outputs/processed/daily_sales.csv`

| Attribute                        |     Result |
| -------------------------------- | ---------: |
| Rows                             |      1,688 |
| Columns                          |          2 |
| First date                       | 2013-01-01 |
| Last date                        | 2017-08-15 |
| Missing values after preparation |          0 |
| Duplicate dates                  |          0 |
| Chronological order              |       True |
| Consecutive daily intervals      |       True |
| Negative daily sales values      |          0 |

The columns are `date` and `daily_sales`. Each row represents the sum of sales across all stores and product families for one calendar day.

### Missing Christmas dates: documented assumption

The four missing dates were matched to national Christmas Day entries in the holiday calendar. The preprocessing code provisionally filled them with zero daily sales so the series has a continuous daily index.

These zero values are **not observed sales values**. The calendar match supports the hypothesis that the dates are absent because of the holiday, but it does not prove the reason. This treatment should be reconsidered before final model training and clearly retained as a limitation.

## 6. Visualisations

EDA figures saved in `outputs/figures/`:

1. `01_sales_distribution.png`
2. `02_daily_sales_trend.png`
3. `03_weekly_sales_patterns.png`
4. `04_top_stores.png`
5. `05_top_product_families.png`
6. `06_holiday_sales_comparison.png`

The prepared daily sales plot is saved as:

- `07_daily_sales_plot.png`

## 7. Task 3 — LSTM Model Development & Training

### Modelling setup

- Notebook: `notebooks/03_lstm_model_development.ipynb`.
- Target: total daily sales across stores and product families.
- Lookback window: 30 previous days to predict the next day.
- Input format: 3D LSTM arrays with one feature per day.
- Scaling: `MinMaxScaler` fitted on the model-training period only.
- Model: one LSTM layer with 32 units, 20% dropout, and one dense output.
- Training: Adam optimiser, MSE loss, MAE metric, validation monitoring, and early stopping.

### Data splits

- Model training: 1,080 observations, producing 1,050 sequences.
- Validation: 270 observations and 270 validation sequences.
- Final test: 338 observations and 338 test sequences.
- Evaluation uses rolling one-day-ahead predictions, where the previous day's actual value is available for the next prediction.

### Test results

| Model          |        MAE |       RMSE |
| -------------- | ---------: | ---------: |
| Naive baseline | 165,347.39 | 227,751.17 |
| LSTM           |  93,248.46 | 148,042.64 |

On this test period, the LSTM reduced MAE by approximately 43.6% and RMSE by approximately 35.0% compared with the naive baseline. This is an encouraging result for the chosen evaluation setup, not a guarantee of performance on other periods.

### Modelling figures

- `outputs/figures/08_lstm_training_validation_loss.png`
- `outputs/figures/09_actual_vs_predicted_sales.png`

### Limitation

The four missing Christmas dates were provisionally filled with zero sales. These are assumed values, not observed sales, and their effect should be considered when interpreting the model results.

## 8. Task 5 — Results Visualisation & Project Delivery

A separate notebook, `notebooks/04_results_visualisation.ipynb`, has been started to compare model metrics and document findings and limitations. The planned comparison chart is `outputs/figures/11_model_performance_comparison.png`. Before delivery, verify that the chart file exists and that its source values match the latest Task 4 evaluation table. The existing prediction-error figure is `outputs/figures/10_lstm_prediction_errors.png`; confirm it is present before relying on it in the README.

## 9. Current Project Status

### Completed

- Project structure and dataset collection.
- Initial exploratory data analysis.
- Six EDA visualisations.
- Data-quality checks and date conversion.
- Daily sales aggregation.
- Investigation of the four missing Christmas dates.
- Continuous daily series construction and validation.
- Prepared CSV export and reload verification.
- Documentation updates for Tasks 1 and 2.

### Remaining

- Review the notebook for redundant cells and ensure all outputs are saved.
- Finalise documentation and dependency versions.
- Commit and push the finished project to GitHub.

## 10. Next Steps

1. Review the notebook and confirm saved outputs.
2. Finalise the README, summary, change log, and requirements.
3. Verify the Task 5 figure and ensure metric values match the latest evaluation output.
4. Commit and push the completed work to GitHub.
5. If the project is extended, revisit the zero-sales assumption for missing Christmas dates and test the model on additional forecasting periods.

## 11. Data and Repository Notes

- Raw CSV files remain local in `datasets/` and are excluded from Git.
- The processed daily series is stored in `outputs/processed/daily_sales.csv`.
- Figures are retained in `outputs/figures/` for use in the README.
- `requirements.txt` lists the libraries used for EDA, preprocessing, modelling, and evaluation.
