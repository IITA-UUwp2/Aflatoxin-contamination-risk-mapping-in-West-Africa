
This project applies a GeoAI approach that combines geospatial machine learning with satellite remote sensing  to predict aflatoxin contamination risk in maize across Nigeria. The goal is to identify high-risk zones and time periods before harvest, supporting early warning systems and targeted mitigation strategies for farmers, policymakers, and food safety stakeholders.

Data

Field samples comprise geotagged maize aflatoxin measurements collected across Nigeria, spanning seven agro-ecological zones (AEZ): Arid/Sahel, Semi-arid/Sudan Savannah, Northern Guinea Savannah, Southern Guinea Savannah, Mid Altitude, Derived Savannah, and Humid Forest. Samples span multiple growing seasons between 2012 and 2024. 

Predictor variables

| Variable | Source | Units |
|---|---|---|
| Precipitation | ERA5-Land | mm |
| Maximum / minimum temperature | ERA5-Land | °C |
| Soil moisture (0–7cm, 7–28cm) | ERA5-Land | m³/m³ |
| Soil temperature (0–7cm, 7–28cm) | ERA5-Land | °C |
| Vapor pressure deficit (VPD) | Derived from ERA5-Land temperature and dewpoint | kPa |
| Palmer Drought Severity Index (PDSI) | TerraClimate | — |
| Enhanced Vegetation Index (EVI) | MODIS | — |
| Elevation | SRTM | m |
| Soil properties (pH, organic carbon, texture) | SoilGrids | — |

All climate predictors are standardized to 9km spatial resolution to match the sample data.

Modelling approach

Predictor variables are matched to field sample records by year and agro-ecological zone and used to train machine learning models to predict aflatoxin contamination levels.

