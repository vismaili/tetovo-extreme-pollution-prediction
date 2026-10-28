# Predicting Extreme Particulate Pollution Events Using Explainable Machine Learning

### A Case Study of Tetovo, North Macedonia

## 1. Project Overview

Air pollution is an important environmental and public health concern in Tetovo, North Macedonia, particularly during periods of elevated particulate matter concentrations.

This project investigates whether machine learning can predict extreme PM2.5 and PM10 pollution conditions using historical air-quality measurements and meteorological variables.

The main objective is to develop classification models capable of identifying whether the average particulate matter concentration during the following 24 hours will exceed a predefined extreme-event threshold.

The study also aims to apply explainable machine learning techniques to better understand the environmental factors associated with extreme pollution conditions.

## 2. Research Objectives

- Analyze historical PM2.5 and PM10 pollution patterns in Tetovo.
- Examine relationships between pollution and meteorological conditions.
- Identify extreme pollution events using a data-driven threshold.
- Develop and compare supervised machine learning classification models.
- Evaluate model performance in detecting extreme pollution periods.
- Use SHAP to interpret the contribution of input variables.

## 3. Dataset

The project uses hourly observations from January 2019 to December 2024.

**Air Quality Data**

Source: Ministry of Environment and Physical Planning, North Macedonia.

Website: https://air.moepp.gov.mk/

Variables:
- PM2.5 concentration
- PM10 concentration

File: `Data(Final).csv`

**Meteorological Data**

Source: ERA5 reanalysis, Copernicus Climate Change Service / ECMWF.

Website: https://cds.climate.copernicus.eu/

Variables:
- Air temperature
- Relative humidity
- Wind speed
- Eastward wind component (u)
- Northward wind component (v)
- Wind direction

File: `Meteo_Data_ERA5.csv`

Original measurement units, station metadata, processing details and dataset redistribution permissions should be verified against source documentation.

## 4. Prediction Task

The project addresses two separate supervised binary classification tasks:

1. Extreme PM2.5 prediction (primary target).
2. Extreme PM10 prediction (secondary target).

At each prediction time, the target is determined from the arithmetic mean of pollutant concentrations over the following 24 hours.

An extreme event is defined when this future 24-hour average exceeds the 90th percentile calculated from the training period.

| Target | Non-extreme (0) | Extreme (1) |
|---|---|---|
| PM2.5 | Future 24-hour mean ≤ threshold | Future 24-hour mean > threshold |
| PM10 | Future 24-hour mean ≤ threshold | Future 24-hour mean > threshold |

The training-period thresholds obtained in the initial analysis are approximately:

- PM2.5: 83.888 µg/m³
- PM10: 104.534 µg/m³

These are dataset-defined thresholds, not official air-quality regulatory limits.

The models will predict extreme-event classifications rather than individual hourly pollutant concentrations.

## 5. Data Preparation

The analysis includes:

- Converting timestamps into datetime format.
- Identifying missing observations and duplicate timestamps.
- Combining air-quality and meteorological datasets.
- Examining variable distributions and unusual measurements.
- Creating historical pollutant lag and rolling-average features.
- Constructing future 24-hour classification labels.
- Comparing historical input variables between extreme and non-extreme periods.

To avoid data leakage, future pollutant measurements are used only to construct target labels and are excluded from model inputs.

## 6. Data Splitting

The dataset is divided chronologically:

| Dataset | Period |
|---|---|
| Training | 2019–2022 |
| Validation | 2023 |
| Testing | 2024 |

Chronological splitting helps evaluate whether the models can generalize to future observations.

## 7. Planned Machine Learning Models

The following classification algorithms are planned for comparison:

- Logistic Regression
- Random Forest
- Support Vector Machine (SVM)
- XGBoost

Model evaluation will focus on average precision, recall, precision and false-positive rates, with particular attention to missed extreme pollution events.

SHAP will be explored to interpret model predictions and identify influential input features.

## 8. Project Structure

```text
tetovo-extreme-pollution-prediction/
│
├── data/
│   ├── Data(Final).csv
│   └── Meteo_Data_ERA5.csv
│
├── notebooks/
│   └── 01_data_description.ipynb
│
├── report.pdf
├── requirements.txt
└── README.md
```

The two CSV files must be placed in the `data/` directory when running the notebook using this structure.

## 9. How to Run

**Step 1:** Clone the repository.

```bash
git clone https://github.com/vismaili/tetovo-extreme-pollution-prediction.git
```

**Step 2:** Open the project directory.

```bash
cd tetovo-extreme-pollution-prediction
```

**Step 3:** Install the required Python packages.

```bash
pip install -r requirements.txt
```

**Step 4:** Open the Jupyter Notebook.

```bash
jupyter notebook notebooks/01_data_description.ipynb
```

**Step 5:** Run all notebook cells in order.

The notebook assumes that the original CSV datasets are located in the project's `data/` directory. File paths may need adjustment if the notebook is run from a different working directory.

## 10. Current Project Status

**Milestone 1 — Project and Data Description**

The initial milestone focuses on defining the prediction problem and exploring the available data.

Completed analyses include dataset inspection, missing-value and duplicate checks, class distribution analysis, majority-class baseline calculations, descriptive statistics and visualizations.

No machine learning model has been trained at this stage.

Future milestones will cover model development, evaluation, comparison and explainability.

## 11. Limitations

The project uses measurements from a single monitoring location and historical ERA5 meteorological data. Its initial evaluation will therefore be retrospective and may not represent operational real-time forecasting performance.

Missing pollution observations, seasonal variation, class imbalance and differences between gridded meteorological data and local conditions are additional limitations that will be considered during model development.

## 12. Academic Information

**Institution:** South East European University  
**Programme:** MSc in Data Science  
**Course:** Machine Learning  
**Group:** G2  
**Study Area:** Tetovo, North Macedonia  
**Study Period:** 2019–2024
