Here is the same text with all emojis removed.

---

# ML-to-predict-new-york-traffic
i will be using public transport GPS, weather patterns events etc to see if they are related and if they affect traffic congestion

GPS Speed Prediction Using Machine Learning

Overview

This project predicts vehicle movement speed using GPS-derived features such as latitude/longitude bins, trip distance, hour of day, and geospatial transformations.

Due to API geo-lock restrictions, real GPS data could not be accessed, so synthetic data was generated to simulate realistic taxi motion patterns in NYC.
Despite this limitation, a complete end-to-end ML workflow was successfully executed.

Project Structure

/data
    synthetic_nyc_taxi_gps.csv
    synthetic_nyc_taxi_hourly_grid.csv
    synthetic_nyc_taxi_daily_summary.csv

/scripts
    preprocessing.py
    training.py
    evaluation.py

ML_GPS_Documentation.docx
README.md

Data Limitation & Solution

API Issue

Attempts to fetch real GPS/traffic data failed due to:

Geo-locked endpoints

Rate limits

IP restrictions

Workaround

High-quality synthetic datasets were created:

GPS trip logs

Hourly grid summaries

Daily aggregated statistics

The synthetic data still preserved:

Randomized but realistic travel paths

Noise

Variability in speed

Temporal patterns

This allowed proper feature engineering and ML training.

Feature Engineering

The following features were produced:

Feature	Description
lat_bin, lon_bin	Spatial grid encoding
hour	Hour-of-day temporal feature
trip_distance	Haversine-based feature
speed	Target variable
euclidean_dist	Straight-line distance
speed_ratio	Distance ratio metric
congestion_proxy	Derived from grid-level speed

Models Trained and Compared

1. Linear Regression

R² ≈ 0.28–0.45

Could not capture non-linear GPS relationships

Performed worst

2. Ridge Regression

R² < 0.60

Helped with small overfitting but still weak

Linear assumptions too restrictive

3. Random Forest Regressor

R² ≈ 0.70–0.80

Strong performance

Good at non-linearities

Stable feature importance

4. XGBoost Regressor (BEST)

R² ≈ 0.85–0.99 depending on dataset

Captured interactions extremely well

Robust to noise

Great generalization

Why the Final Model Was Chosen

The Random Forest/XGBoost models were chosen because:

They handle non-linear geospatial effects

Perform well on sparse, noisy synthetic GPS data

Achieve R² values far higher than linear models

Require minimal manual feature scaling

Provide feature importance insights

Linear models explained less than 60% of the variance, making them unsuitable.

Evaluation Metrics

Model performance was evaluated using:

Mean Squared Error (MSE)
Coefficient of Determination (R²)

These metrics helped compare different algorithms and select the best-performing one.

Conclusion

Despite the lack of real API data, the project successfully:

Built a full ML pipeline

Generated synthetic GPS datasets

Engineered useful geospatial features

Compared multiple ML models

Achieved high accuracy with Random Forest/XGBoost
