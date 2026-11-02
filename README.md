# Energy-Emissions-SQL-and-Time-Series Project

## Overview
Analysis of U.S. electricity demand, generation, and CO2 emissions using SQL and time series modeling. Joined four database tables, modeled emissions with linear regression, and forecasted emissions with an ARIMA model.

## Data
- SQLite database (`energy.db`) with monthly U.S. data in four tables: emissions, demand, CO2 intensity, and electricity generation
- Data for 2025 only runs through May
- Units differ across tables: demand and generation in TWh, emissions in mtCO2, CO2 intensity in gCO2/kWh

## Steps Performed
- Queried the database with SQL, using JOINs across four tables to combine emissions, demand, CO2 intensity, and generation by date
- Created total emissions and total generation columns directly in the SQL query
- Plotted 2025 trends for all four measures
- Split the data by time: trained on years before 2022, tested on 2022 onward
- Fit a linear regression to predict total emissions from demand, CO2 intensity, and generation
- Decomposed the series with STL, then checked stationarity with the Augmented Dickey-Fuller test
- Used ACF and PACF plots, QQ plots, and AIC comparison to choose ARIMA(3,0,2)
- Forecast one month ahead at a time with an expanding training window

## Results
- Linear Regression: about 2.75% MAPE on the test set
- ARIMA(3,0,2): about 8% MAPE on the test set
- In 2025, all four measures declined early in the year and rose by the end of the available data
- Total demand and total electricity generation followed nearly identical patterns

## Tools & Libraries
- Python
- SQLite (sqlite3)
- pandas
- NumPy
- scikit-learn
- statsmodels
- Matplotlib

## Key Takeaway
Linear regression using demand, CO2 intensity, and generation predicted emissions more accurately (about 2.75% error) than the ARIMA forecast (about 8% error), likely because those inputs are directly tied to emissions, while ARIMA only uses the past values of emissions itself.
