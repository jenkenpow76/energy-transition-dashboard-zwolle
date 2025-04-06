# energy-transition-dashboard-zwolle
This repository contains a complete pipeline for processing, cleaning, and analyzing  datasets at the neighborhood level. It also contains scripts used for Geographically weihhted regression and Agent Based Model.  

#  Clean Energy Data Processing Project
This project focuses on processing, cleaning, enriching, and analyzing clean energy and subsidy data at the neighborhood level. It involves multiple stages of data transformation, from raw data ingestion to geocoding and mapping.

##  Notebooks Overview
Each notebook performs a specific data cleaning or transformation step:

| Notebook                                | Description                                      |
|-----------------------------------------|--------------------------------------------------|
| `01_cleanEnergyCoaching.ipynb`          | Cleans and standardizes energy coaching data     |
| `02_clean_SDESubsidy.ipynb`             | Processes SDE subsidy information                |
| `03_clean_SCESubsidy.ipynb`             | Cleans SCE subsidy records                       |
| `04_clean_ISDESubsidy.ipynb`            | Standardizes ISDE subsidy datasets               |
| `05_cleanDemographicBuurt.ipynb`        | Integrates demographic data at neighborhood level |
| `06_cleanEnergyConsumptionBuurt.ipynb`  | Processes energy consumption by neighborhood     |
| `07_cleanBuildings.ipynb`               | Cleans building-related data                     |
| `08_Add_Neighbourhood to csvs.ipynb`    | The data is mapped to neighbourhoods     |
| `09_clean_localSubsidy.ipynb`           | Handles local subsidy datasets                   |

## Tools & Technologies
- Python 
- Jupyter Notebooks
- CSV & GeoJSON formats
## Spatial Modeling: Geographically Weighted Regression (GWR)

This includes a reproducible workflow for applying Geographically Weighted Regression (GWR) to assess how energy policies and demographic factors influence gas consumption at the neighborhood level.

GWR is a spatial regression technique that allows model relationships to vary over space, capturing local variations that traditional global models (like Ordinary Least Squares) may miss. This is especially relevant for understanding the localized effects of energy subsidies and coaching programs across different neighborhoods.

### Purpose

The GWR analysis is used to explore:
- How policy interventions (like subsidies or coaching) relate to energy consumption behavior.
- Whether those relationships vary by neighborhood, reflecting spatial heterogeneity.
- How spatially explicit modeling can support more targeted and equitable energy transitions.

### Workflow Overview

**Data Preparation**
- Merging cleaned datasets: demographics, buildings, subsidies, coaching
- Aggregation and filtering by year (2015–2023)
- Spatial integration using neighborhood centroids

**Variable Selection**
- Feature engineering from housing, income, and energy datasets
- Multicollinearity checks (Variance Inflation Factor & correlation analysis)

**Model Construction**
- Standardizing predictors via Z-score transformation
- Assigning spatial coordinates for each neighborhood
- Applying GWR using an adaptive bandwidth and bisquare kernel
- Separating policy variables (e.g., subsidies, coaching) from control variables

**Diagnostics & Validation**
- Assessing model assumptions and preparing residuals for spatial analysis
- Ensuring the approach is robust to year-over-year differences in data availability

### Required Libraries

The modeling pipeline is implemented in Python using the following libraries:

| Category           | Libraries Used                                      |
|--------------------|-----------------------------------------------------|
| Data Manipulation  | pandas, numpy                                       |
| Spatial Data       | geopandas, shapely, libpysal, esda                  |
| Preprocessing      | sklearn.preprocessing                               |
| GWR Modeling       | mgwr, spglm                                         |
| Visualization      | matplotlib, seaborn                                 |

You can install them using: pip install pandas numpy geopandas shapely libpysal esda scikit-learn mgwr spglm matplotlib seaborn

### Reproducibility

- The GWR modeling is fully contained in the notebook:   `Subsidies and Coaching Effect GWR.ipynb`
- Data is pre-cleaned and joined in earlier scripts in this repository.
- Spatial geometries are derived from shapefiles included in the data pipeline.
- The code is modular and can be extended to other municipalities or spatial units.


