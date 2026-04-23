# flood-risk-uk
Flood risk prediction for UK regions


UK Flood Prediction model

# Project Outline


## OBJECTIVE

Flood risk predictor (probability, severity, and) in the UK
* Automated pipeline pulling UK weather + river data
* Clean feature store (S3/parquet)
* Model predicting flood risk per region
* Dashboard showing:
    * Map of UK with risk scores
    * Time-based trends

Compare:
* Predicted vs actual floods
Show:
* Where model performs well / poorly


Granularity (per):
* postcode 
* Grid cell 
* River basin
* Town
Time Horizon: 
* Short term (24-48 hours)
* Seasonal
Impact: 
* Communities affected
* Infrastructure affected
* Financial impact

## Data Sources ## 

Static Data:
* DEM Data
* Distance to Rivers
* Soil Type / Permeability
* Land use (urban vs rural)

Dynamic
* Rainfall (historical + forecasted)
* River level
* Saturation
* Temperature

UK Data Sources
* Environmental Agency (flood + river data)
* UK Met Office (weather)
* Copernicus (Satellite + rainfall)

## Data Pipeline

Ingestion: 
* Batch pull APIs
* Datasets

Storage:
* raw -> silver -> gold
Transformation:
* feature engineering (e.g. rolling rainfall, lag features)
Structure:
    /data
        /raw
        /processed
        /feaures


## Features Layer ##

This feeds dashboards and Model Features

Analytic:
* Aggregated rainfall (24h, 72h, etc.)
* Flood event labels
* Regional summaries
* Time-series metrics

Model Features:
* Aggregated rainfall (24h, 72h, etc.)
* Rolling Rainfall
* River level change rate
* Elevation gradient
* Distance to nearest body of water


## Model

Baseline:
* Logistic Regression (classification flood/no flood)
    
Intermediate:
* XGBoost
* Random Forest 

Advanced:
* Spatio-temporal models
* LSTM (for sequence modelling)


## Evaluation

Metrics:
* ROC-AUC
* Precision/Recall (important for rare events)

Backtesting:
* Train on past → predict known flood events


## Output / Product Layer

Output analysis:
* Risk scores by region
* Visualisation:
    * Map-based flood risk dashboard
* Optional:
    * Alert system (e.g., “high risk in next 48h”)

## Deployment

Batch Pipeline (Daily Predictions)
Store Outputs
Serve via dashboard or APIs



# TECH STACK

## Dev
* Python and VS Code


## Storage 

AWS S3 bucket 
* raw / structured / features 
* parquet files

## Data Pipeline Orchestration

* Python scripts + cron 
* add Apache later Airflow

## Modelling
* scikit-learn
* tensorflow
* XGBoost

## Visualisation 
* Power BI
* Streamlit app (more advanced)

## Optional
Geo tools:
* geopandas
* shapely
APIs:
* FastAPI (serve predictions)
* Experiment tracking:
* MLflow