What each file is

File naming: precip_growing_season_AEZ_<year>.tif — one file per sample year (2012, 2013, 2015, 2016, 2017, 2018, 2024).

What's inside each file: a single multi-band raster covering all of Nigeria at 9km resolution, where each band represents one specific (AEZ zone × time period) combination for that file's year. Two types of bands exist:

Monthly bands — one per month that falls within a given AEZ's growing season, for that year. Band name pattern:
   precip_<AEZname>_<year>_m<monthNumber>

Example: precip_HumidForest_2018_m5 = total precipitation (mm) in the Humid Forest zone, May 2018, summed across the month.

Seasonal bands — one per AEZ, summarizing the entire growing season as a single total. Band name pattern:
   precip_<AEZname>_<year>_seasonal

Example: precip_HumidForest_2018_seasonal = total precipitation (mm) across Humid Forest's entire growing season (March–December) in 2018.

What a pixel value actually means

Every pixel in every band is total precipitation in millimeters, summed over that band's specific time window (one month, or the whole growing season), at that pixel's location.
A pixel outside a given band's AEZ zone will be blank/no-data, since each band is clipped to just its own zone's boundary 
