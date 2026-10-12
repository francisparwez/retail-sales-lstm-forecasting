# Change Log

This file records significant changes, completed tasks, and project milestones.

## [2026-10-11] — Task 1: Project Setup & Exploratory Data Analysis

### Added

- Initial project structure for the retail sales forecasting project.
- `notebooks/01_exploratory_data_analysis.ipynb`.
- `outputs/figures/` for saved EDA visualisations.
- Six figures covering sales distribution, daily trends, weekday patterns, top stores, top product families, and holiday/event comparison.

### Analysis completed

- Loaded and inspected `train.csv`.
- Reviewed dimensions, columns, data types, missing values, and date coverage.
- Calculated descriptive sales statistics.
- Explored daily and weekly sales patterns.
- Compared cumulative sales across stores and product families.
- Conducted a preliminary comparison of holiday/event dates against other dates.

### Data management

- Kept raw CSV datasets in the local `datasets/` directory.
- Excluded raw CSV files from Git tracking.
- Retained EDA figures in the repository for README display.

## [2026-10-11] — Task 2: Data Preprocessing & Time Series Preparation

### Added

- `notebooks/02_data_preprocessing.ipynb`.
- `outputs/figures/07_daily_sales_plot.png` for the prepared daily sales series.
- `outputs/processed/daily_sales.csv` containing the prepared daily sales series.

### Data preparation

- Loaded the training dataset and inspected data types, missing values, duplicate rows, and date coverage.
- Converted the `date` column to datetime.
- Aggregated sales across all stores and product families into one daily total.
- Compared observed dates with a complete daily calendar.
- Identified four missing dates: 25 December 2013, 2014, 2015, and 2016.
- Matched those dates to national Christmas Day entries in `holidays_events.csv`.
- Created a continuous series with 1,688 daily observations from 2013-01-01 to 2017-08-15.
- Provisionally filled the four missing dates with zero sales and documented that this is an assumption rather than observed sales.
- Validated missing values, duplicate dates, chronological order, negative sales, and daily intervals.
- Saved the processed CSV, reloaded it, and checked that dates matched and sales values matched within floating-point tolerance.

### Documentation

- Updated the README to describe Tasks 1 and 2, the prepared series, the file structure, and the missing-date assumption.
- Updated the project summary to include preprocessing results and next steps.

## [2026-10-12] — Task 3: LSTM Model Development & Training

### Added

- `notebooks/03_lstm_model_development.ipynb`.
- A naive rolling one-day-ahead baseline forecast.
- A 30-day sequence preparation workflow with training-only scaler fitting.
- An LSTM model with 32 units, dropout, a dense output, and early stopping.
- `outputs/figures/08_lstm_training_validation_loss.png`.
- `outputs/figures/09_actual_vs_predicted_sales.png`.

### Model evaluation

- Evaluated 338 test-period predictions using MAE and RMSE.
- Naive baseline: MAE 165,347.39; RMSE 227,751.17.
- LSTM: MAE 93,248.46; RMSE 148,042.64.
- In this test period, the LSTM reduced MAE by approximately 43.6% and RMSE by approximately 35.0% compared with the baseline.
- Evaluation represents rolling one-day-ahead predictions, not a single multi-day forecast generated in advance.

### Limitations and documentation

- Retained the documented caveat that four Christmas dates were provisionally filled with zero sales.
- Updated the project status and results for final documentation and repository delivery.

---

## Upcoming work

- Final review of notebook cells, saved outputs, and documentation.
- Commit and push the completed project to GitHub.
