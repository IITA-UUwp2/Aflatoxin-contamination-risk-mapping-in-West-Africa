\# Aflatoxin Contamination Risk Mapping in West Africa



\## Overview



Aflatoxins are toxic secondary metabolites produced by \*Aspergillus flavus\* and related fungi, contaminating staple crops such as maize under favourable climatic conditions. Exposure poses significant risks to human and animal health, including liver cancer, immune suppression, and impaired growth in children. This repository documents a GeoAI and remote sensing workflow for mapping aflatoxin contamination risk in maize across two West African countries: Nigeria and Ghana.



The work integrates georeferenced field sample data with satellite-derived climate, soil, and vegetation predictors to model and map spatial variation in aflatoxin contamination risk, in support of early warning and targeted mitigation strategies.



\## Countries



\- \*\*\[Nigeria/](./Nigeria)\*\* — Machine learning-based aflatoxin risk prediction using field samples and ERA5-Land climate data extracted per agro-ecological zone and growing season.

\- \*\*\[Ghana/](./Ghana)\*\* — Aflatoxin contamination analysis using field samples and environmental data.



\## Methodology summary



Predictor variables (precipitation, temperature, soil moisture, soil temperature, vapor pressure deficit, and others) are extracted from satellite and reanalysis data sources using Google Earth Engine, standardized to a common spatial resolution, and matched to field-collected aflatoxin sample data by year and agro-ecological zone.



\## Structure



Each country folder contains its own scripts, extracted data, and documentation. See each folder's README for project-specific methodology and status.

