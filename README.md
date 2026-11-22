# FBI Crime Time Series Forecasting

Forecasts monthly crime incident counts for each crime type using seasonal
SARIMA models.

## Problem
Given historical crime records, predict the number of incidents per month and
per crime type for a future test period. This supports planning and monitoring
by showing which crime categories may rise or fall.

## Dataset
- `Train.xlsx`: about 475,000 incident records (13 columns, including crime
  TYPE, YEAR, MONTH, location and time fields).
- `Test.csv`: 162 rows of YEAR, MONTH and TYPE for which incident counts are
  predicted.

## Approach
1. Load the train and test files and check shapes, missing values and duplicates.
2. Build a monthly date column from YEAR and MONTH.
3. Aggregate incidents by month and crime type.
4. Reindex to a complete monthly time series, filling missing months with 0.
5. Explore the data: crime type distribution, monthly totals, top crime types.
6. Fit a separate SARIMA(1,1,1)(1,1,1,12) model for each crime type, with a
   fallback to the historical mean when a series is short or the model fails.
7. Generate predictions in the submission format (YEAR, MONTH, TYPE,
   Incident_Counts).

## Results
Validation on the last 6 months for one sample crime type
(Break and Enter Commercial):

| Metric | Value |
|--------|-------|
| MAE    | 25.17 |
| RMSE   | 29.08 |

## Tech stack
Python, Pandas, NumPy, Statsmodels, Scikit-learn, Matplotlib, Seaborn,
Google Colab

## How to run
1. Open the notebook in Google Colab.
2. Upload `Train.xlsx` and the test CSV to the Colab files area.
3. Update the file paths in the loading cell if your file names differ.
4. Run all cells. The predictions are saved as `submission.csv`.

## Limitations
- Validation was done on one crime type only, not all categories.
- The same SARIMA settings are used for every crime type; tuning per category
  could improve accuracy.
- Duplicate rows were checked but not removed before counting incidents.

## Author
Vidya, [github.com/Vidya-imp](https://github.com/Vidya-imp)
