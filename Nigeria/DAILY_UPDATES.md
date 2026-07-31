# Daily Updates 
### 2026-07-31
-Built and ran the GEE script for AEZ-based static elevation extraction from USGS SRTM. One band per AEZ, clipped to AEZ geometry.
-Verified elevation output in ArcGIS Pro
-Built and ran the GEE script for AEZ-based static soil properties extraction from SoilGrids (ISRIC): pH, SOC, and clay (as the texture proxy), top 2 depth layers (0-5cm, 5-15cm) for each. No year loop, same static pattern as elevation.
-Verified soil properties output in ArcGIS Pro; confirmed SoilGrids stores values as scaled integers (e.g. pH x10) and noted the need to apply the correct scaling factor per property before use in R.
-Built and ran the GEE script for AEZ-based growing-season EVI extraction from MODIS (MOD13Q1), following the VPD/precipitation pattern (monthly bands + seasonal mean). Added a quality-masking step using the SummaryQA band (masking out anything not flagged 0/good quality) before aggregating, and applied MODIS's x0.0001 scaling factor to convert stored values to real EVI units.
-Built and ran the GEE script for AEZ-based growing-season PDSI extraction from TerraClimate, same monthly + seasonal structure. TerraClimate provides PDSI directly; applied the x0.01 scaling factor to convert stored values to real PDSI units.
-All 9 predictor variables are now complete: precipitation, temperature, VPD, soil moisture, soil temperature, elevation, soil properties, EVI, and PDSI.
Next: run spatial thinning and then move to extraction

### 2026-07-28

- Built, debugged, and ran the GEE script for AEZ-based growing-season precipitation extraction from ERA5-Land, monthly bands per growing-season month plus one seasonal aggregate band, per AEZ, per sample year. Restructured the export to run per-year (instead of one combined export) to resolve a GEE payload-size limit error.
- Verified the 2024 precipitation output in ArcGIS Pro,values correctly clipped per AEZ zone and physically sensible. Found ERA5-Land's native precipitation units are in meters; decided to convert precipitation (and other volume-based variables going forward) to millimeters at export time for direct readability.
- Built, debugged, and ran the GEE script for max/min temperature extraction, following the same AEZ/per-year structure. Used true seasonal extremes (max of monthly tmax, min of monthly tmin) for the seasonal aggregate, rather than an average.
- Verified the temperature output the same way, confirming Kelvin-to-Celsius conversion and sensible values per zone/month.
- Reorganized the GitHub repo's raster outputs into `raster_prep/precipitation/` and `raster_prep/temperature/` subfolders 
- Next: soil moisture and soil temperature (both directly available from ERA5-Land, same script pattern), then VPD (already scripted, not yet run), then the non-ERA5-Land variables (PDSI, EVI, elevation, soil properties).
- 
### 2026-07-27
- Started Step 2 of the workflow: GEE raster preparation, independent of the still-blocked point dataset restart.
- Reviewed Stella's older GEE variable-extraction code as a reference. 
- Built a GEE script for AEZ-based growing-season precipitation extraction from ERA5-Land:
  - Uses the AEZ growing-season table (Francis/Tofa) to determine which months to pull per zone.
  - Produces both monthly bands (one per growing-season month, per AEZ, per year) and a seasonal aggregate band (one per AEZ, per year).
  - Debugged several script issues along the way (case-sensitivity typos, misplaced export call, AEZ name spelling mismatches).
- Hit and resolved a GEE export payload size limit by restructuring the script to build and export one GeoTIFF per sample year (7 files: 2012, 2013, 2015, 2016, 2017, 2018, 2024) instead of one combined file.
- Verified the 2024 output in ArcGIS Pro: raster values are correctly clipped to each AEZ zone's boundary, and values are physically sensible once accounting for ERA5-Land's precipitation units (meters, not millimeters).
- Next: replicate this pattern for the remaining predictor variables (VPD, temperature, soil moisture, etc.)

***Added .tif files for precipitation***
File naming: precip_growing_season_AEZ_<year>.tif , one file per sample year (2012, 2013, 2015, 2016, 2017, 2018, 2024).
What's inside each file: a single multi-band raster covering all of Nigeria at 9km resolution, where each band represents one specific (AEZ zone × time period) combination for that file's year. Two types of bands exist:
1. Monthly bands :one per month that falls within a given AEZ's growing season, for that year. Band name pattern:
   precip_<AEZname>_<year>_m<monthNumber>
Example: precip_HumidForest_2018_m5 = total precipitation (mm) in the Humid Forest zone, May 2018, summed across the month.

2. Seasonal bands: one per AEZ, summarizing the entire growing season as a single total. Band name pattern:
   precip_<AEZname>_<year>_seasonal
Example: precip_HumidForest_2018_seasonal = total precipitation (mm) across Humid Forest's entire growing season (March–December) in 2018.


### 2026-07-24
- Redid the AEZ and State spatial join independently (using the actual AEZ shapefile and a GADM Nigeria states boundary) and got identical gaps to the original join.  
- 26 codes have no AEZ match; 6 of those also have no State match.
- Resolved the 6 missing-State codes manually via LGA lookup (Jibia → Katsina State; Bosso → Niger State).
- The remaining 26 AEZ-missing codes are mostly Niger Delta coastal/market towns (Bonny, Abonema, Akuku-Toru) and Lagos coastal LGAs (Ibeju-Lekki, Eti-Osa, Lekki, Amuwo Odofin)

### 2026-07-23
- Restarted the cleaning process from the original raw dataset
- Found that 192 sample codes (546 records) appear more than once in the raw data ,the same sample code entered multiple times, sometimes with different years or coordinates attached.
- Cleaned this up by only merging entries where the code, year, and coordinates all matched exactly (treating anything less than a full match as a genuine question mark rather than assuming it's safe to merge).
- This removed 242 records that were confirmed duplicate re-entries of the same sample, bringing the dataset down to 2,401 clean records.
- 112 sample codes (224 records) are still flagged as unresolved conflicts, split into two types:
    - 67 codes where the same sample appears twice with the same location and aflatoxin level but a different year recorded.
    - 45 codes where the same sample appears twice with both the year and the location different between entries, but similar aflatoxin level.
- Received the growing-season table (planting/harvest windows by agro-ecological zone) from Francis, sourced from Tofa's November 2025 data. 
-Recently cleaned file now titled 'Afl_new_deduped'
