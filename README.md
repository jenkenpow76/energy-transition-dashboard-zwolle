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
| `08_Add_Neighbourhood to csvs.ipynb`    | Adds neighborhood codes to all relevant data     |
| `09_clean_localSubsidy.ipynb`           | Handles local subsidy datasets                   |

## Tools & Technologies

- Python 
- Jupyter Notebooks
- CSV & GeoJSON formats



