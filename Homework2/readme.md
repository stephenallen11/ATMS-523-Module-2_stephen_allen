ds_europe# Climate Teleconnection Analysis

Analyzes atmospheric teleconnection patterns associated with extreme daily precipitation events in London using ERA5 reanalysis data.

## Overview

The script performs 6 stages:
1. **Load London Data** - Downloads ERA5 precipitation for London 5×5° box (2010-2024)
2. **Calculate Extremes** - Finds 95th percentile threshold and plots CDF
3. **Load Europe Data** - Downloads Europe region data for extreme days
4. **Calculate Anomalies** - Computes departures from 1981-2020 climatology  
5. **Create Maps** - Generates composite precipitation maps
6. **Summary** - Prints analysis results

## Requirements

```
dask
xarray
pandas
numpy
matplotlib
cartopy
```

## Installation

```bash
pip install dask xarray pandas numpy matplotlib cartopy
```

## Usage

```bash
python climate_analysis.py
```

## Data Sources

- **ERA5 Hourly Data**: Google Cloud public dataset (gs://gcp-public-data-arco-era5)
- **ERA5 Climatology**: University of Illinois (1981-2020 monthly means)

## Output Files

- `london_precipitation_timeseries.csv` - London daily precipitation time series
- `london_precipitation_cdf.png` - CDF plot showing 95th percentile threshold
- `london_extreme_precip_composite_maps.png` - Europe composite maps for extreme days
- `ERA-5_total_precipitation_monthly-1981-2020.nc` - Downloaded climatology

## Configuration

Modify these constants at the top of the script:

```python
LONDON_LAT, LONDON_LON = 51.5, -0.1    # London coordinates
LAT_MIN, LAT_MAX = 50.0, 55.0           # London analysis box
LON_MIN, LON_MAX = -5.0, 0.0
```

## Analysis Regions

- **London Box**: 50°N-55°N, 5°W-0°E (5×5 degrees)
- **Europe Region**: 40°N-70°N, 20°W-20°E (~3000×2500 km)

## Technical Details

- Uses `dask` through xarray's chunked loading for efficient memory management
- Processes ~14 years of hourly data converted to daily means
- Identifies extreme events (≥95th percentile) and creates composite patterns
- Computes anomalies relative to long-term climatology

## Performance

- Requires stable internet connection for cloud data access
- Memory usage optimized through dask chunking
- Runtime: ~10-30 minutes depending on network speed
- Processes ~5TB of source data efficiently through chunking

## Notes

- All precipitation values converted to mm/day
- Uses 95th percentile threshold to define extreme events
- Composite shows average European precipitation patterns during London extreme days
- Reveals potential atmospheric teleconnections across Europe