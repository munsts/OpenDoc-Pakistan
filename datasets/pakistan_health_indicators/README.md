# Pakistan National Health Indicators (Time Series)

## Summary

This dataset is a long-format annual time series of Pakistan's core public-health indicators, compiled from the World Bank Open Data / World Development Indicators (WDI) API. It covers mortality, life expectancy, fertility, nutrition (stunting), non-communicable disease burden, health expenditure, and cause-of-death composition from 1960 to 2024. It is designed for machine-learning forecasting, trend analysis, and public-health research on Pakistan.

## Dataset Details

- **Dataset ID**: `pakistan-health-indicators`
- **Version**: `1.0.0`
- **Category**: `Health`
- **Tags**: `health`, `public-health`, `indicators`, `mortality`, `life-expectancy`, `time-series`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan (national aggregate)`
- **Time Period**: `1960 - 2024`
- **File Formats**: `CSV`
- **Records**: `472 observations across 14 indicators`
- **Update Frequency**: `Annual`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: World Bank Open Data — World Development Indicators (WDI)
- **Source URL**: https://data.worldbank.org/country/pakistan
- **Source Type**: Public open-data API (`https://api.worldbank.org/v2/country/PAK/indicator/...`)
- **Collection Method**: Programmatic download of per-indicator JSON responses (country=PAK), filtered to non-null observations.
- **Collection Date**: July 2026
- **Processing Pipeline**: Merged per-indicator responses into a single long-format table (`indicator_code, indicator_name, year, value, unit`), dropped null values, added human-readable unit labels, sorted by indicator and year.
- **Raw Data Availability**: Fully public via the World Bank API.

## License

- **Original License**: CC BY 4.0 (World Bank Open Data Terms of Use)
- **Repository License**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Redistribution**: Allowed
- **Restrictions**: Must credit the World Bank and OpenDoc Pakistan.

## Intended Use

Appropriate for:
- Time-series forecasting of mortality, life expectancy, and health-expenditure trends.
- Benchmarking Pakistan against regional or global health-indicator baselines.
- Feature engineering for socio-economic and public-health ML models.

## Out-of-Scope Use

- Sub-national (provincial/district) analysis — values are national aggregates.
- Real-time or current-year decisions — the latest year may lag or be provisional.

## Data Structure

Single CSV at `data/processed/health_indicators.csv` in long format. One row per indicator per year.

Indicators included: life expectancy at birth, infant mortality, under-5 mortality, maternal mortality ratio, total fertility rate, current health expenditure (% GDP), out-of-pocket expenditure (% of health spend), under-5 stunting, diabetes prevalence, communicable-disease share of deaths, hospital beds (per 1,000), physicians (per 1,000), births attended by skilled staff, and basic drinking-water access.

## Data Dictionary

See [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 100 / 100
- **Rating**: Excellent
- **Missing Values**: Null observations removed; coverage varies by indicator and year.
- **Duplicate Rows**: 0% (primary key: `indicator_code` + `year`).
- **Validation Status**: Passed Frictionless tabular-data-resource schema.
- **Known Issues**: Some indicators (e.g. maternal mortality, stunting) are modelled estimates or survey-year points rather than continuous annual measurements.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (aggregate national statistics, no personal data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None

## Bias, Gaps, and Limitations

- National aggregates hide large provincial and urban/rural disparities.
- Older values (1960s–1980s) rely on sparser measurement and modelled back-estimates.

## Example Usage

```python
import pandas as pd

df = pd.read_csv("data/processed/health_indicators.csv")

# Life expectancy trend
le = df[df["indicator_code"] == "SP.DYN.LE00.IN"]
print(le[["year", "value"]].tail(10))
```

## Citation

```text
World Bank, "World Development Indicators — Pakistan", curated as "Pakistan National Health Indicators" by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
