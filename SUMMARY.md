# Project Summary

## 1. Project Overview

**Project title:** Predictive Analytics on Retail Sales: Time Series Forecasting with LSTM

**Dataset:** Kaggle Store Sales – Time Series Forecasting

**Business context:** Historical retail sales forecasting using data from Corporación Favorita in Ecuador.

**Current stage:** Tasks 1 and 2 — Project Setup, Exploratory Data Analysis, and Data Preprocessing & Time Series Preparation completed.

The project explores historical sales patterns and prepares a daily sales series for the next forecasting stages. A baseline and LSTM will be developed and compared later.

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

## 7. Current Project Status

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

- Define the forecasting horizon and evaluation strategy.
- Create chronological training, validation, and test splits.
- Establish a baseline forecast.
- Prepare sequential input windows.
- Build and train the LSTM model.
- Compare model performance with the baseline.
- Visualise forecasts and document final conclusions.

## 8. Next Steps

1. Decide the forecast horizon and evaluation period before modelling.
2. Revisit the zero-sales assumption for missing Christmas dates.
3. Define chronological training, validation, and test periods to avoid data leakage.
4. Build a simple baseline forecast.
5. Prepare sequential inputs for the LSTM.
6. Evaluate forecasts using metrics such as MAE and RMSE.
7. Compare the LSTM with the baseline and document limitations.

## 9. Data and Repository Notes

- Raw CSV files remain local in `datasets/` and are excluded from Git.
- The processed daily series is stored in `outputs/processed/daily_sales.csv`.
- Figures are retained in `outputs/figures/` for use in the README.
- `requirements.txt` currently lists the libraries used in Tasks 1 and 2; modelling dependencies will be added when required.
