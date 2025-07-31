### EV Vehicle Charge Demand Prediction

## Overview
This repository contains a Streamlit web application for forecasting electric vehicle (EV) adoption trends in Washington State counties over a 3-year horizon. It uses a RandomForestRegressor model trained on historical EV data with engineered features to predict cumulative EV counts, offering interactive visualizations and multi-county comparisons. The project was developed as part of the AICTE Internship Cycle 2 by S4F.
Table of Contents

## Project Description
Dataset
Installation
Usage
Model Details
Features
Results
Contributing
License
Contact

## Project Description
The EV Adoption Forecaster is a Streamlit-based tool designed to predict EV adoption trends for counties in Washington State. It leverages a pre-trained RandomForestRegressor model to forecast monthly EV counts based on historical data, with visualizations for single-county trends and comparisons across up to three counties. The project includes data preprocessing, feature engineering, and model evaluation scripts to support accurate forecasting.

## Dataset
The dataset (preprocessed_ev_data.csv) contains historical EV adoption data for Washington State counties, with the following key columns:

Date: Timestamp of the data point (converted to datetime).
County: Name of the county.
State: State identifier (e.g., WA).
Electric Vehicle (EV) Total: Number of EVs registered.
Battery Electric Vehicles (BEVs): Count of BEVs.
Plug-In Hybrid Electric Vehicles (PHEVs): Count of PHEVs.
Non-Electric Vehicle Total: Count of non-EVs.
Total Vehicles: Total vehicle count.
Percent Electric Vehicles: Percentage of EVs among total vehicles.
county_encoded: Label-encoded county identifier.
months_since_start: Time index since the earliest data point per county.
Lagged Features: ev_total_lag1, ev_total_lag2, ev_total_lag3 (1-, 2-, and 3-month lagged EV totals).
Rolling Mean: ev_total_roll_mean_3 (3-month rolling mean of EV totals).
Percentage Changes: ev_total_pct_change_1, ev_total_pct_change_3 (1- and 3-month percentage changes).
Growth Slope: ev_growth_slope (6-month rolling linear slope of cumulative EV growth).

# Note:
The dataset is not included in the repository due to its size. Contact the repository owner for access or use a compatible dataset.

## Installation

# Clone the repository:
git clone https://github.com/grk1102/EV_Vehicle_Charge_Demand_Prediction.git
cd EV_Vehicle_Charge_Demand_Prediction


# Install dependencies:
Ensure Python 3.8+ is installed,
then install the required packages:
pip install -r requirements.txt

# The requirements.txt includes:
numpy==1.26.4
pandas==1.5.3
scikit-learn==1.6.1
scipy==1.15.2
statsmodels==0.14.4
streamlit==1.44.1
tensorflow==2.19.0


# Prepare the model and data:

Place the pre-trained model (forecasting_ev_model.pkl), dataset (preprocessed_ev_data.csv), and image (ev-car-factory.jpg) in the project directory.
Update file paths in app.py if necessary (default paths assume local storage).



# Usage

Run the prototype code (optional, for model training and preprocessing):

Execute the prototype script to preprocess data, train the RandomForestRegressor model, and generate visualizations:python prototype.py


Outputs include preprocessed_ev_data.csv, forecasting_ev_model.pkl, and plots (stacked_column_chart.png, kings_forecast.png, kings_cumulative.png, top_5_counties.png).


# Run the Streamlit app:
streamlit run app.py


Access the app in a web browser (typically at http://localhost:8501).
Select a county to view its 3-year EV adoption forecast with a cumulative trend plot.
Use the multi-select option to compare trends across up to three counties.
View growth percentage estimates and interactive visualizations.



## Model Details

# Model:
RandomForestRegressor with hyperparameter tuning via RandomizedSearchCV.
Input Features:
months_since_start: Time index per county.
county_encoded: Label-encoded county identifier.
ev_total_lag1, ev_total_lag2, ev_total_lag3: 1-, 2-, and 3-month lagged EV totals.
ev_total_roll_mean_3: 3-month rolling mean of EV totals.
ev_total_pct_change_1, ev_total_pct_change_3: 1- and 3-month percentage changes in EV totals.
ev_growth_slope: 6-month rolling linear slope of cumulative EV growth.


# Target:
Electric Vehicle (EV) Total (monthly EV count).
Evaluation Metrics: Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), R² Score.
Forecast Horizon: 36 months (3 years).

## Features

# Data Preprocessing:
Handles missing values, converts data types, caps outliers in Percent Electric Vehicles, and creates time-series features (lags, rolling mean, percentage changes, growth slope).
# Single County Forecast:
Displays historical and forecasted cumulative EV trends for a selected county, with growth percentage estimates.
# Multi-County Comparison:
Compares cumulative EV adoption trends for up to three counties in a single plot.
# Visualizations:
Matplotlib-based plots (e.g., stacked bar charts for EV types, cumulative trend plots) with a dark theme in the Streamlit app.
# User Interface: 
treamlit app with a gradient background, custom styling, and an EV-related image (ev-car-factory.jpg).

## Results

The RandomForestRegressor model provides accurate EV adoption forecasts, evaluated using MAE, RMSE, and R² metrics.
The Streamlit app generates interactive plots showing historical and forecasted cumulative EV counts, with growth percentages (e.g., "30.25% increase 📈" for a county).
Visualizations include a stacked column chart for BEV/PHEV breakdown and top-5 county trends.
