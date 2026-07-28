# Max/Min Temperature Rasters: Growing Season, by AEZ

## What this data is

For each agro-ecological zone (AEZ) in Nigeria, and for each year we have aflatoxin samples from, this shows the maximum and minimum air temperature during that zone's growing season, pulled from ERA5-Land satellite/reanalysis climate data.

Each zone has its own growing season (e.g. Sahel: June–September, Humid Forest: March–December) So the temperature data is only pulled for the months that are actually relevant to that zone's crop cycle, not the whole year.

## What's inside each file

One file per year (2012, 2013, 2015–2018, 2024). Inside each file, every zone gets:

- **A tmax and tmin value for each month** in its growing season (e.g. "Humid Forest, May 2018: tmax = 32°C, tmin = 21°C")
- **One seasonal tmax and tmin**, the single hottest and single coldest monthly values across that zone's whole growing season, not an average

## Why both monthly and seasonal

This feeds into comparing three modelling approaches: one using the monthly detail, one using just the seasonal summary, and one using both, to see whether the extra month-by-month detail actually improves predictions over the simpler seasonal number.

## Units

Degrees Celsius. Resolution is 9km
