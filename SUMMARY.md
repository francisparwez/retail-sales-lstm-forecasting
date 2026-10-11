# Project Summary

## 1. Project Overview

**Project title:** Predictive Analytics on Retail Sales: Time Series Forecasting with LSTM

**Dataset:** Kaggle Store Sales – Time Series Forecasting

**Business context:** Historical retail sales forecasting using data from Corporación Favorita in Ecuador.

**Current stage:** Task 1 — Project Setup & Exploratory Data Analysis completed.

The project aims to investigate historical sales patterns, prepare a forecasting dataset, establish a baseline, and evaluate whether an LSTM neural network can produce useful sales forecasts.

## 2. Dataset Overview

The initial analysis was performed on `train.csv`.

| Attribute                           |     Result |
| ----------------------------------- | ---------: |
| Total rows                          |  3,000,888 |
| Total columns                       |          6 |
| First date                          | 2013-01-01 |
| Last date                           | 2017-08-15 |
| Unique dates                        |      1,684 |
| Unique stores                       |         54 |
| Product families                    |         33 |
| Missing values in inspected columns |          0 |

### Columns

- `id` — row identifier.
- `date` — date of the sales observation.
- `store_nbr` — store identifier.
- `family` — product family.
- `sales` — sales value.
- `onpromotion` — number of items on promotion, as represented in the dataset.

The initial inspection found no missing values in the six columns. Further validation will be needed when the data is prepared for forecasting.

## 3. Descriptive Sales Statistics

| Statistic            |                 Result |
| -------------------- | ---------------------: |
| Total sales          |       1,073,644,952.20 |
| Mean sales per row   |                 357.78 |
| Median sales per row |                  11.00 |
| Minimum sales        |                   0.00 |
| Maximum sales        |             124,717.00 |
| Standard deviation   | Approximately 1,102.00 |

The mean is substantially higher than the median, and the maximum is much larger than a typical observation. This indicates a strongly right-skewed sales distribution.

These observations should be investigated in context. High values should not automatically be removed, because they may represent genuine sales activity.

## 4. Key EDA Findings

### Sales distribution

Sales are strongly right-skewed. The difference between the mean and median suggests that relatively high sales observations influence the overall distribution.

### Daily sales trend

Aggregated daily sales show fluctuations and an overall upward pattern across the observed period. Additional analysis is needed to separate long-term trends from recurring calendar effects and other influences.

### Weekly sales patterns

The initial weekday comparison shows relatively high aggregated sales on Saturday and Sunday, with Thursday lower in the current analysis. This pattern should be re-examined during time series preparation.

### Store performance

Store 44 has the highest cumulative sales among the top stores displayed in the EDA comparison. Store-level differences may be relevant when deciding how to construct the forecasting dataset.

### Product-family performance

The leading product families by cumulative sales are:

1. GROCERY I
2. BEVERAGES
3. PRODUCE

These categories may be useful candidates for further investigation, but their ranking alone does not establish which product families are easiest to forecast.

### Holiday and event dates

The preliminary comparison reported the following average daily sales:

| Date category                       |   Average daily sales |
| ----------------------------------- | --------------------: |
| Dates not marked as holidays/events | Approximately 627,548 |
| Dates marked as holidays/events     | Approximately 694,431 |

Average daily sales were higher on dates marked as holidays or events in this comparison. This is a descriptive association, not proof of causation. The comparison does not control for seasonality, event type, store closures, or other factors.

## 5. Visualisations Generated

The EDA notebook generated six figures in `outputs/figures/`:

1. `01_sales_distribution.png`
2. `02_daily_sales_trend.png`
3. `03_weekly_sales_patterns.png`
4. `04_top_stores.png`
5. `05_top_product_families.png`
6. `06_holiday_sales_comparison.png`

These figures are referenced in the project README.

## 6. Current Project Status

### Completed

- Initial project setup and folder structure.
- Collection of the initial dataset files.
- Loading and inspection of the training dataset.
- Review of data types, missing values, and date coverage.
- Descriptive sales statistics.
- Six EDA visualisations.
- Initial interpretation of sales distribution, trends, weekly patterns, store performance, product-family performance, and holiday/event comparisons.
- Initial project documentation.

### Not yet completed

- Data preprocessing and time series preparation.
- Selection of the forecasting target and horizon.
- Chronological training, validation, and test splits.
- Baseline forecasting.
- LSTM model development and training.
- Model evaluation and optimisation.
- Final forecast visualisations and conclusions.

## 7. Next Steps

1. Inspect the supporting datasets and determine which features are appropriate for the forecasting objective.
2. Define the sales target, aggregation level, and forecast horizon.
3. Convert and validate date fields, and investigate relevant data-quality issues.
4. Design chronological training, validation, and test splits to avoid future information leaking into training.
5. Establish a simple baseline forecast.
6. Prepare sequential data for LSTM training.
7. Evaluate the LSTM against the baseline using appropriate metrics, including MAE and RMSE.
8. Document results, limitations, and conclusions based on the measured performance.

## 8. Important Notes

- The current findings describe the initial EDA; they are not final modelling conclusions.
- Raw CSV files remain local and are excluded from Git tracking.
- The holiday/event comparison is preliminary and should not be interpreted causally.
- No claim has been made that an LSTM will outperform a simpler forecasting approach. That conclusion must be based on evaluation results.
