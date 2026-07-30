# Soil Temperature Rasters: Growing Season, by AEZ

ERA5-Land soil temperature (layers 1 & 2), extracted per AEZ growing season, per sample year (2012, 2013, 2015–2018, 2024). One GeoTIFF per year, all 7 zones bundled together.

## Bands

- **Monthly:** `soil_tempL1_<AEZ>_<year>_m<month>`, `soil_tempL2_<AEZ>_<year>_m<month>` — one pair per growing-season month.
- **Seasonal:** `soil_tempL1_<AEZ>_<year>_seasonal`, `soil_tempL2_<AEZ>_<year>_seasonal` — average across the growing season.

## Layers

L1 = 0–7cm depth, L2 = 7–28cm depth.

## Units

Degrees Celsius (converted from ERA5-Land's native Kelvin).

## Resolution

9km, clipped per AEZ boundary, EPSG:4326.

## Source

`soil_temperature_level_1` / `soil_temperature_level_2`, `ECMWF/ERA5_LAND/MONTHLY_AGGR`.

##
