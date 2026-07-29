### Field Sites Spatial Mapping and Standardization
This repository contains a systematic mapping of all locations visited during data collection, along with the standardization procedure applied to the dataset.
The data was collected between **6th and 12th July 2026** in **Western Kenya**, by a team led by **Dr. Francis (IITA)**.
## GPS Data Structuring -LVB Scoping Study
### Source Data
Raw GPS points were collected as an unstructured `.txt` file containing 28 site locations across the Lake Victoria Basin (LVB) region of Western Kenya, with fields for Name, Latitude, Longitude, and Address separated by inconsistent whitespace.
### Standardization Method
The raw text was parsed and structured using **R** (run via the `rpy2` R-magic extension in Google Colab):
1. Read the raw file line-by-line with `readLines()`, skipping the header row.
2. Split each line into fields using a regular expression on runs of 2 or more spaces (`\\s{2,}`), which reliably separated columns while preserving single spaces within multi-word names and addresses (e.g., "Budalagi Samia resort").
3. Assembled the split fields into a structured `data.frame` with four columns: `Name`, `Latitude`, `Longitude`, `Address` — coercing coordinates to numeric type.
4. Validated the parse by checking for rows with `NA` latitude/longitude (indicating a split failure) — none found across all 28 rows.
5. Exported the cleaned data to `.csv`.
### Mapping Output
The structured coordinates were used to produce GPS point maps of the study sites across Busia, Kakamega, Vihiga, Siaya, Kisumu, Homa Bay, and Kericho counties (Western Kenya, bordering Lake Victoria).
Rather than grouping sites by county, points were classified by the sub-basin of the Lake Victoria Basin in which they fall — namely the **Sio, Nzoia, Yala, Nyando, and Sondu** sub-basins — reflecting the hydrological rather than administrative context of the study sites.The maps were exported in both PDF and PNG formats.
