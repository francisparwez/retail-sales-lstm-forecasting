# Change Log

This file records significant changes, completed tasks, and project milestones.

## [2026-10-11] — Task 1: Project Setup & Exploratory Data Analysis

### Added

- Initial project structure for the retail sales forecasting project.
- `notebooks/01_exploratory_data_analysis.ipynb` for exploratory data analysis.
- `outputs/figures/` directory for saving EDA visualisations.
- Six visualisations covering:
  - Sales distribution.
  - Daily sales trends.
  - Weekly sales patterns.
  - Top-performing stores.
  - Top product families.
  - Holiday/event sales comparison.
- `SUMMARY.md` to record the current findings and project status.
- `requirements.txt` for the libraries used in the current analysis.

### Analysis completed

- Loaded and inspected `train.csv`.
- Reviewed dataset dimensions, columns, data types, missing values, and date coverage.
- Calculated descriptive sales statistics.
- Aggregated sales to explore daily and weekly patterns.
- Compared cumulative sales across stores and product families.
- Conducted a preliminary comparison of holiday/event dates against other dates.

### Documentation

- Updated `README.md` to reflect the completed EDA, current findings, visualisations, and remaining workflow.
- Documented the distinction between descriptive observations and conclusions that require further investigation.

### Data management

- Kept raw CSV datasets in the local `datasets/` directory.
- Continued excluding raw CSV files from Git tracking to avoid committing large data files.
- Retained generated visualisations in the repository for use in the README.

### Pending

- Data preprocessing and time series preparation.
- Definition of the forecasting target and horizon.
- Chronological training, validation, and test splits.
- Baseline forecasting implementation.
- LSTM development, training, and evaluation.
- Final results, limitations, and conclusions.

---

## Upcoming milestones

Future entries will be added when the following tasks are completed:

- **Task 2:** Data Preprocessing & Time Series Preparation.
- **Task 3:** LSTM Model Development & Training.
- **Task 4:** Model Evaluation & Optimisation.
- **Task 5:** Results Visualisation & Project Delivery.
