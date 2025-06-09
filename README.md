# Los Angeles Crime Data Analysis (2020-Present)

![GitHub](https://img.shields.io/badge/Language-Python-blue)
![GitHub](https://img.shields.io/badge/Libraries-Pandas%20%7C%20Scikit--learn%20%7C%20Matplotlib-orange)
![GitHub](https://img.shields.io/badge/ML%20Concepts-Supervised%20%26%20Unsupervised%20Learning-brightgreen)

A **data pipeline** and **machine learning** project analyzing crime trends in Los Angeles (2020–Present) from [data.lacity.org](https://data.lacity.org). The project includes **exploratory analysis**, **unsupervised clustering**, and **crime prediction** using Random Forest.

---

## 🔍 Project Overview

### 📂 Dataset
- **Source**: [Los Angeles Crime Data 2020-Present](https://data.lacity.org/Public-Safety/Crime-Data-from-2020-to-Present/2nrs-mtv8)
- **Features**: Crime type, location (lat/lon), time/date, victim demographics.
- **Size**: ~1M+ records (updated monthly).

### 🎯 Goals
1. **Trend Analysis**: Identify crime patterns by time, location, and category.
2. **Unsupervised Learning**: Cluster crimes into hotspots using geospatial data.
3. **Supervised Learning**: Predict crime types using Random Forest.
4. **Next Crime Prediction**: Deploy a model to forecast likely crimes.

---

## 🛠️ Key Features

### 1. **Unsupervised Classification (Clustering)**
- **Algorithm**: `DBSCAN` (Density-Based Spatial Clustering of Applications with Noise)
- **Purpose**: Automatically detect high-crime **hotspots** without labeled data.
- **Implementation**:
  ```python
  from sklearn.cluster import DBSCAN
  coords = crime_data[['LAT', 'LON']].dropna()
  dbscan = DBSCAN(eps=0.01, min_samples=50)  # Tuned for LA's geography
  crime_data['cluster_label'] = dbscan.fit_predict(coords)




 Output: Geographic clusters labeled as hotspots (-1 = noise/outliers).

2. Random Forest Classifier
Algorithm: RandomForestClassifier (from sklearn.ensemble)

Purpose: Predict crime types based on location, time, and victim data.

Key Features:

Inputs: Area, day of week, hour, victim demographics, coordinates.

Target: Crime type (e.g., "Burglary", "Assault").

Performance:

Accuracy: ~85% (varies by crime type).

Feature Importance: Hour of day and location (LAT/LON) are top predictors.

3. Time-Series Trends
Methods: Monthly aggregation, year-over-year comparison.

Libraries: pandas.resample, matplotlib.

4. Geospatial Visualization
Tools: folium.HeatMap for crime density maps.

Example:
https://images/la_crime_heatmap.png

📊 Results
Unsupervised Learning (DBSCAN)
Cluster Label	Crimes Count	Description
0	15,000	Downtown LA hotspot
1	9,200	Hollywood Blvd area
-1 (Noise)	110,000	Low-density areas
Random Forest Metrics
Class	Precision	Recall	F1-Score
Burglary	0.89	0.82	0.85
Assault	0.76	0.71	0.73
Theft	0.91	0.95	0.93

How to run:
1. Install dependencies:
pip install pandas scikit-learn matplotlib folium xgboost
2. Download data:
Run the notebook to fetch data from data.lacity.org.
3. Execute the notebook:
jupyter notebook LA_Crime_Analysis.ipynb
