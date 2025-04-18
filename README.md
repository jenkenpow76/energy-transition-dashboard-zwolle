![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-F37626?logo=jupyter)
![GAMA](https://img.shields.io/badge/AgentBasedModel-GAMA-lightgrey?logo=gamedev)
![License](https://img.shields.io/badge/License-MIT-green)
<p align="right">
  <img src="assests/utwente_logo.png" width="200"/>
</p>


# Energy Transition Dashboard – Zwolle

This repository presents a complete, modular workflow for building a neighborhood-level **energy transition dashboard** for the municipality of Zwolle. It integrates **data cleaning**, **spatial analysis**, and **agent-based simulation modeling** to explore how energy policies like subsidies and coaching programs impact local energy consumption.

The project combines:

- **Python-based data processing and modeling**
- **Geographically Weighted Regression (GWR)** for spatial analytics
- An **Agent-Based Model (ABM)** built in **GAMA Platform** for interactive simulation

It is designed for researchers, policy analysts, and planners interested in localized climate interventions and spatial decision-making.

---

## Python Environment

- Python version: `3.12.7`
- Install all dependencies via:

```
pip install -r Requirements.txt
```

---



## 1. Datasets

| **Dataset**                                 | **Source**                          | **Format** | **Description**                                                                 | **Use**                                                                                   |
|--------------------------------------------|-------------------------------------|------------|---------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| Digitale Tweelingstad Zwolle Adressen 2D   | ArcGIS Online                                   | Map          | 2D digital twin of Zwolle                                                      | Building energy label, renewable energy category                                           |
| Thema's Buurten 2015–2023                  | [Cijfers Over Zwolle](https://www.zwolle.nl) | Excel      | Social, demographic, and energy indicators at the neighborhood level           | Cleaned and renamed columns, extracted indicators, merged with geographic data            |
| Buurtgrenzen Zwolle                        | [CBS](https://www.cbs.nl) / [Gemeente Zwolle](https://www.zwolle.nl) | Shapefile  | Spatial boundaries of neighborhoods                                            | Primary spatial join layer; used for mapping and aggregating by neighborhood and district |
| Coachgesprekken HOOMdossier                | Stakeholder from Blauwvinger Energie | Excel      | Number and type of energy coaching sessions                                   | Geocoded postcodes; aggregated by neighborhood and district; spatial coaching distribution |
| SDE                                         | [RVO](https://www.rvo.nl)           | CSV        | Production-based renewable energy subsidies                                    | Spatial join and aggregation for neighborhood-level regression and visualization          |
| SCE                                         | [RVO](https://www.rvo.nl)           | CSV        | Subsidy for local energy cooperatives                                          | Spatial join and aggregation for neighborhood-level regression and visualization          |
| ISDE                                        | [RVO](https://www.rvo.nl)           | CSV        | Investment subsidy for sustainable heat                                        | Geocoded postcodes; spatial join; aggregated for neighborhood analysis                     |
| SPUK (WOZ subsidies)                       | Stakeholder from Zwolle Municipality | CSV        | Local subsidies (often tied to property values/WOZ)                            | Geocoded postcodes; aggregated by neighborhood; used in regression and visualization       |
| Energy Consumption                          | [Climate Monitor](https://klimaatmonitor.databank.nl) / [RVO](https://www.rvo.nl) | CSV | Energy use and gas consumption data                                            | Used in regression analysis on gas consumption                                             |
                              

## 2. Clean Energy Data Processing

This step prepares the base datasets used in GWR and mapping.

### Notebooks Overview

| Notebook                                | Description                                      |
|-----------------------------------------|--------------------------------------------------|
| `01_cleanEnergyCoaching.ipynb`          | Cleans and standardizes energy coaching data     |
| `02_clean_SDESubsidy.ipynb`             | Processes SDE subsidy information                |
| `03_clean_SCESubsidy.ipynb`             | Cleans SCE subsidy records                       |
| `04_clean_ISDESubsidy.ipynb`            | Standardizes ISDE subsidy datasets               |
| `05_cleanDemographicBuurt.ipynb`        | Integrates demographic data at neighborhood level|
| `06_cleanEnergyConsumptionBuurt.ipynb`  | Processes energy consumption by neighborhood     |
| `07_cleanBuildings.ipynb`               | Cleans building-related data                     |
| `08_Add_Neighbourhood to csvs.ipynb`    | Maps cleaned data to neighborhood geometries     |
| `09_clean_localSubsidy.ipynb`           | Handles local subsidy datasets                   |

---

## 3. Spatial Modeling: Geographically Weighted Regression (GWR)

This section includes a reproducible workflow for applying **Geographically Weighted Regression (GWR)** to evaluate the spatial impact of policy variables (e.g. subsidies, coaching) on neighborhood gas consumption.

GWR accounts for spatial heterogeneity, unlike traditional models, by allowing relationships to vary across space.

### Workflow

- Merge and clean policy + demographic data (2015–2023)
- Feature selection using correlation and VIF filtering
- Calculate neighborhood centroids from shapefiles
- Standardize features (Z-score) and apply `mgwr` GWR model
- Assess residuals and model stability over time

### Libraries Used

| Category           | Libraries Used                                      |
|--------------------|-----------------------------------------------------|
| Data Manipulation  | pandas, numpy                                       |
| Spatial Data       | geopandas, shapely, libpysal, esda                  |
| Preprocessing      | scikit-learn                                        |
| GWR Modeling       | mgwr, spglm                                         |
| Visualization      | matplotlib, seaborn                                 |

Install:

```
pip install pandas numpy geopandas shapely libpysal esda scikit-learn mgwr spglm matplotlib seaborn
```

### Reproducibility

- Main notebook: `Subsidies and Coaching Effect GWR.ipynb`
- Fully integrated with output from the cleaning pipeline
- Easily extendable to other municipalities or policy contexts

---

## 4. Agent-Based Simulation: Interactive Energy Policy Model (GAMA)

This model, developed in **GAMA Platform v1.9.1**, simulates how buildings respond to subsidy incentives over time. It provides an interactive way to experiment with policy configurations such as subsidy rates and eligibility thresholds.

### Purpose

- Explore the long-term effects of subsidy programs
- Allow stakeholders to test policy scenarios
- Visualize spatial dynamics in building upgrades and energy use

### Model Structure

- `building`: Each building has its own budget, energy use, and decision rules
- `road`: Used for spatial display
- Spatial inputs: `building.shp`, `road.shp`, and `bounds.shp`
  
Make sure the following files are present in the `data/` folder:
- `building.shp`, `building.shx`, `building.dbf`
- `road.shp`, `road.shx`, `road.dbf`
- `bounds.shp`, `bounds.shx`, `bounds.dbf`


### Decision-Making Logic

- Each year, eligible buildings may be selected for upgrade
- Upgrades reduce energy consumption by 30%
- Decisions are **stochastic**, meaning based on a probability to reflect real-world uncertainty

 ### Policy Logic

- At the start of each year, a fixed number of eligible buildings are selected.
- If the subsidy is available and the building owner has enough budget, upgrades are applied.
- Upgrades reduce a building’s energy consumption by 30%.
- Stakeholders can adjust policy parameters in real time using sliders and checkboxes in the GUI.


### Running the Model

1. **Install GAMA Platform**  
   Download from: [https://gama-platform.org](https://gama-platform.org)

2. **Open GAMA**  
   - Go to `File > Import > Existing Projects into Workspace`
   - Select the folder containing the `.project`, `models/`, and `data/` directories

3. **Load the Model**  
   - Open the file `energy_policy_model.gaml` inside the `models/` folder

4. **Run the Experiment**  
   - Select the experiment named `energy_policy` and press **Run**
   - Adjust parameters interactively using the sidebar controls



### GUI Parameters

| Parameter                         | Description                                      |
|----------------------------------|--------------------------------------------------|
| `Subsidy Rate`                   | Percent of cost covered by policy                |
| `Upgrade Cost`                   | Total cost to upgrade a building                 |
| `Max Subsidized Buildings`       | Max buildings upgraded per year                  |
| `Subsidy Available`              | Enable/disable subsidy                           |
| `Subsidy End Year`               | Year when subsidy ends                           |

### Outputs

- 2D visualization of building upgrades
- Time series chart of energy consumption
- Monitors for policy and simulation status

---

## Project Folder Structure

| Folder / File                         | Description                                       |
|--------------------------------------|---------------------------------------------------|
| `raw_data/`                           | Raw input files (subsidies, demographics, GIS)    |
| `clean_data/`                         | Cleaned and processed datasets                    |
| `aggregated_data/`                    | Final merged datasets                             |
| `geocoded_data/`                      | Files enriched with spatial coordinates           |
| `mapped_data/`                        | Datasets joined with geometry                     |
| `minimized_data/`                     | Streamlined datasets for modeling                 |
| `scripts/`                            | Jupyter notebooks (1–9)                           |
| `Geographically weighted Regression/` | GWR notebook and scripts                          |
| `Agent Based Model/`                  | GAMA model files                                  |
| `data/`                               | Shapefiles required by the GAMA model             |
| `requirements.txt`                    | Python dependencies                               |


---

## License

MIT License

---

## Acknowledgments

This project was created in fulfillment of the **Climate Transition** module within the **IJssel Delta Project** at the University of Twente. It is part of the Master's program in **Spatial Engineering**.

We would like to acknowledge the support of our instructors and peers who contributed feedback throughout the development process.

---

## Contact

For questions, feedback, or collaboration opportunities, please reach out:

- k.o.herl@student.utwente.nl  
- j.k.powers@student.utwente.nl  
- y.k.ongera@student.utwente.nl
