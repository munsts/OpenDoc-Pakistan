# Pakistan Macroeconomic Indicators (2010–2025)

## Summary

This dataset compiles key annual macroeconomic indicators for Pakistan from the year 2010 to 2025. It tracks GDP growth percentage, consumer price index (CPI) inflation, exports, imports, worker remittances, and the unemployment rate. This dataset is essential for economic researchers, policy analysts, and data science students studying inflation cycles, trade deficits, and growth trends.

## Dataset Details

- **Dataset ID**: `pakistan-macroeconomic-indicators`
- **Version**: `1.0.0`
- **Category**: `Economy and Finance`
- **Tags**: `economics`, `gdp`, `inflation`, `trade`, `remittances`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan (national scale)`
- **Time Period**: `2010 - 2025`
- **File Formats**: `CSV`
- **Size**: `1 KB`
- **Update Frequency**: `Annually`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: State Bank of Pakistan (SBP) & Pakistan Bureau of Statistics (PBS)
- **Source URL**: https://www.sbp.org.pk
- **Source Type**: Official Central Bank and Bureau of Statistics publications
- **Collection Method**: Digitized and consolidated from historical annual reports and economic surveys.
- **Collection Date**: January 2026
- **Processing Pipeline**: Consolidated tabular listings, adjusted columns to consistent scale (Billions USD), and compiled into standard CSV.
- **Raw Data Availability**: Publicly available on SBP and PBS websites.

## License

- **Original License**: Public Domain (State Bank of Pakistan open release)
- **Repository License**: Open Data Commons Public Domain Dedication and License (PDDL)
- **Attribution Required**: Recommended (Optional)
- **Commercial Use**: Allowed
- **Redistribution**: Allowed
- **Restrictions**: None.

## Intended Use

Appropriate for:
- Building macroeconomic forecasting models (e.g., predicting inflation based on import levels).
- Analyzing the historical impact of workers' remittances on national economic indicators.
- Historical trend visualization.

## Out-of-Scope Use

Prohibited or discouraged uses:
- Real-time stock trading or short-term investment advising (this dataset has annual resolution).
- Micro-economic or corporate finance analysis (the indicators are macro-aggregate).

## Data Structure

The dataset contains a single CSV file under `data/processed/macroeconomic_indicators.csv`.
Columns:
- `year` (integer): Calendar year of observation.
- `gdp_growth_pct` (number): Real GDP growth rate percentage.
- `cpi_inflation_pct` (number): Average consumer price index inflation percentage.
- `exports_billion_usd` (number): Total goods and services exports in billions of USD.
- `imports_billion_usd` (number): Total goods and services imports in billions of USD.
- `remittances_billion_usd` (number): Worker remittances inflows in billions of USD.
- `unemployment_rate_pct` (number): Estimated percentage of the labor force that is unemployed.

## Data Dictionary

Detailed field definitions are available in [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 100 / 100
- **Rating**: Excellent
- **Missing Values**: 0%
- **Duplicate Rows**: 0%
- **Validation Status**: Passed
- **Known Issues**: None.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (No personal data; national aggregates)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None.
- **Reviewer**: OpenDoc Compliance Board
- **Review Date**: July 3, 2026

## Bias, Gaps, and Limitations

- Data for the final year (2025) contains provisional estimates released by the SBP, subject to adjustments in subsequent economic surveys.
- Parallel exchange markets (e.g., open market vs interbank rates) are not modeled in the trade indicators.

## Example Usage

```python
import pandas as pd
import matplotlib.pyplot as plt

# Load dataset
df = pd.read_csv("data/processed/macroeconomic_indicators.csv")

# Plot GDP growth vs Inflation over years
plt.plot(df["year"], df["gdp_growth_pct"], label="GDP Growth %")
plt.plot(df["year"], df["cpi_inflation_pct"], label="CPI Inflation %")
plt.legend()
plt.title("GDP Growth vs Inflation in Pakistan")
plt.show()
```

## Citation

Please cite this dataset as:
```text
State Bank of Pakistan, "Pakistan Macroeconomic Indicators (2010–2025)", curated by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
