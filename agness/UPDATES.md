# Daily Updates — Agness



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
- -Added the generated .tif files to the git repo


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
