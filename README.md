# energy-transition-dashboard-zwolle
This repository contains data and scripts for modelling the Energy Coaching and Subsidies Dashboard for the Municipality of Zwolle.

Datasets
### Datasets Used

| Dataset | Source | Format | Description | Use |
|--------|--------|--------|-------------|-----|
| Thema's Buurten 2015–2023 (one file for each year) | Gemeente Zwolle | Excel | Contains social, demographic, and energy indicators at the neighborhood level | - Cleaned and renamed columns<br>- Extracted relevant indicators<br>- Merged with geographic data |
| Buurtgrenzen Zwolle | CBS / Gemeente Zwolle | Shapefile | Spatial boundaries of neighborhoods | - Used as the primary spatial join layer<br>- Used for mapping and aggregating results per neighborhood and district |
| Coachgesprekken HOOMdossier | HOOMdossier | Excel | Number and type of energy coaching per buurt | - Geocoded the postcodes<br>- Aggregated sessions by neighborhood and district<br>- Used to analyze spatial coaching distribution |
| SDE | Gemeente Zwolle | CSV | SDE subsidy applications (production-based renewable energy) | - Added neighborhood information through spatial join<br>- Aggregated by neighborhood for analysis<br>- Used in regression and visualization |
| SCE | Gemeente Zwolle | CSV | Subsidy for local energy cooperatives | - Added neighborhood information through spatial join<br>- Aggregated by neighborhood for analysis<br>- Used in regression and visualization |
| ISDE | Gemeente Zwolle | CSV | Investment subsidy for sustainable heat | - Geocoded the postcodes<br>- Added neighborhood information through spatial join<br>- Aggregated by neighborhood for analysis<br>- Used in regression and visualization |
| SPUK (Local Subsidies known as WOZ) | Gemeente Zwolle | CSV |  | - Geocoded the postcode<br>- Aggregated by neighborhood for analysis<br>- Used in regression and visualization |
