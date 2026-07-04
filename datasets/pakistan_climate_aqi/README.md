# Pakistan Climate and Air Quality Index (AQI) 2025

## Summary

This dataset compiles monthly average temperature, rainfall, and Air Quality Index (AQI) values (including PM2.5 concentrations and primary pollutants) across major provincial capitals of Pakistan for the first half of 2025 (January to May). It is valuable for environmental researchers, climatologists, and public health analysts studying smog cycles in Lahore and surrounding cities.

## Dataset Details

- **Dataset ID**: `pakistan-climate-aqi`
- **Version**: `1.0.0`
- **Category**: `Climate and Environment`
- **Tags**: `climate`, `weather`, `air-quality`, `aqi`, `smog`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan (Lahore, Karachi, Islamabad, Peshawar, Quetta)`
- **Time Period**: `January 2025 - May 2025`
- **File Formats**: `CSV`
- **Size**: `1 KB`
- **Update Frequency**: `Monthly`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: Pakistan Environmental Protection Agency (Pak-EPA) & Provincial EPAs
- **Source URL**: https://momet.gov.pk
- **Source Type**: Public environmental monitoring dashboards & meteorological announcements
- **Collection Method**: Aggregated from EPA air quality trackers and Pakistan Meteorological Department (PMD) summaries.
- **Collection Date**: January 2026
- **Processing Pipeline**: Standardized dates to ISO 8601, aligned city names, and structured air quality metrics.
- **Raw Data Availability**: Publicly visible on EPA portals.

## License

- **Original License**: Open Government Data License (OGDL) Pakistan
- **Repository License**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Redistribution**: Allowed
- **Restrictions**: Must credit EPAs, PMD, and OpenDoc Pakistan.

## Intended Use

Appropriate for:
- Smog analysis and seasonal air quality comparisons in major cities.
- Training machine learning models to forecast PM2.5 levels based on temperature and rain.
- Policy research for urban development and environment regulations.

## Out-of-Scope Use

Prohibited or discouraged uses:
- Real-time weather forecasting or health advisory alerts (the data is historical and aggregated).
- Direct micro-climate modeling within specific city neighborhoods (the data is city-wide average).

## Data Structure

The dataset contains a single CSV file under `data/processed/climate_aqi.csv`.
Columns:
- `city` (string): Major city name.
- `date` (date): Date of observation (YYYY-MM-DD).
- `avg_temp_c` (number): Average temperature in degrees Celsius.
- `rainfall_mm` (number): Total monthly rainfall in millimeters.
- `aqi_value` (integer): Air Quality Index value.
- `pm25_concentration` (number): PM2.5 concentration in micrograms per cubic meter (µg/m³).
- `primary_pollutant` (string): Primary air pollutant detected.

## Data Dictionary

Detailed field definitions are available in [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 96 / 100
- **Rating**: Excellent
- **Missing Values**: 0%
- **Duplicate Rows**: 0%
- **Validation Status**: Passed
- **Known Issues**: Climate readings for Quetta may occasionally experience sensor gaps in weather stations during severe frost.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (No personal data; fully public environment data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None.
- **Reviewer**: OpenDoc Compliance Board
- **Review Date**: July 3, 2026

## Bias, Gaps, and Limitations

- Only the 5 main administrative hubs of Pakistan are represented in this early version.
- AQI standards map to US-EPA standard equations, which are adapted by provincial EPAs.

## Example Usage

```python
import pandas as pd

# Load dataset
df = pd.read_csv("data/processed/climate_aqi.csv")

# Filter for Lahore smog details
lahore_data = df[df["city"] == "Lahore"]
print(lahore_data[["date", "aqi_value", "pm25_concentration"]])
```

## Citation

Please cite this dataset as:
```text
Pakistan EPA & PMD, "Pakistan Climate and Air Quality Index (AQI) 2025", curated by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
