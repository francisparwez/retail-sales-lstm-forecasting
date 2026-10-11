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

### Pending

- Define the forecast target horizon and chronological validation strategy.
- Establish a baseline forecast.
- Prepare sequential input windows.
- Develop and train the LSTM.
- Evaluate the LSTM against the baseline.
- Document final results and limitations.

---

## Upcoming milestones

- **Task 3:** LSTM Model Development & Training.
- **Task 4:** Model Evaluation & Optimisation.
- **Task 5:** Results Visualisation & Project Delivery.
