# Pakistan Disease Surveillance and Immunization Coverage (Time Series)

## Summary

This dataset is a long-format annual time series of Pakistan's communicable-disease burden and childhood immunization coverage, compiled from the World Bank Open Data / World Development Indicators (WDI) API. It tracks vaccine coverage (measles, DPT, hepatitis B, polio), malaria incidence, and HIV prevalence. It supports epidemiological trend analysis and ML forecasting of vaccine coverage and disease incidence in Pakistan — an epidemiologically important country as one of the last polio-endemic states.

## Dataset Details

- **Dataset ID**: `pakistan-disease-surveillance`
- **Version**: `1.0.0`
- **Category**: `Health`
- **Tags**: `disease`, `surveillance`, `immunization`, `vaccine`, `polio`, `malaria`, `hiv`, `measles`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan (national aggregate)`
- **Time Period**: `1980 - 2024`
- **File Formats**: `CSV`
- **Records**: `242 observations across 7 indicators`
- **Update Frequency**: `Annual`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: World Bank Open Data — World Development Indicators (WDI)
- **Source URL**: https://data.worldbank.org/country/pakistan
- **Source Type**: Public open-data API (`https://api.worldbank.org/v2/country/PAK/indicator/...`)
- **Collection Method**: Programmatic download of per-indicator JSON responses (country=PAK), filtered to non-null observations.
- **Collection Date**: July 2026
- **Processing Pipeline**: Merged per-indicator responses into a single long-format table, dropped null values, added unit labels, sorted by indicator and year.
- **Raw Data Availability**: Fully public via the World Bank API. Underlying figures originate from WHO/UNICEF (immunization) and WHO Global Health Observatory (malaria, HIV).

## License

- **Original License**: CC BY 4.0 (World Bank Open Data Terms of Use)
- **Repository License**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Redistribution**: Allowed
- **Restrictions**: Must credit the World Bank, WHO/UNICEF, and OpenDoc Pakistan.

## Intended Use

Appropriate for:
- Forecasting childhood immunization coverage and identifying coverage gaps.
- Studying long-run trends in malaria incidence and HIV prevalence.
- Public-health policy research and dashboards.

## Out-of-Scope Use

- Sub-national outbreak tracking or case-level surveillance — values are national annual aggregates.
- Clinical or individual-level decisions.

## Data Structure

Single CSV at `data/processed/disease_surveillance.csv` in long format. One row per indicator per year.

Indicators: measles immunization (% 12–23 months), DPT immunization (% 12–23 months), hepatitis B immunization (% one-year-olds), polio immunization (% one-year-olds), malaria incidence (per 1,000 at risk), HIV prevalence (% ages 15–49), and tuberculosis incidence (per 100,000).

## Data Dictionary

See [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 100 / 100
- **Rating**: Excellent
- **Missing Values**: Null observations removed; coverage varies by indicator start year.
- **Duplicate Rows**: 0% (primary key: `indicator_code` + `year`).
- **Validation Status**: Passed Frictionless tabular-data-resource schema.
- **Known Issues**: Immunization coverage figures are WHO/UNICEF estimates (WUENIC) and may be revised retrospectively; malaria/HIV values are modelled.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (aggregate national statistics, no personal data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None

## Bias, Gaps, and Limitations

- National aggregates obscure provincial disparities (e.g. polio and measles risk concentrate in specific districts).
- Estimation methods differ across indicators, limiting cross-indicator comparability.

## Example Usage

```python
import pandas as pd

df = pd.read_csv("data/processed/disease_surveillance.csv")

# Measles immunization coverage over time
meas = df[df["indicator_code"] == "SH.IMM.MEAS"]
print(meas[["year", "value"]].tail(10))
```

## Citation

```text
World Bank / WHO / UNICEF, "World Development Indicators — Pakistan (health)", curated as "Pakistan Disease Surveillance and Immunization Coverage" by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
