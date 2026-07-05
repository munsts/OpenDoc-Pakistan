# Pakistan Macroeconomic Indicators (Time Series)

## Summary

This dataset is a long-format annual time series of Pakistan macroeconomic indicators compiled from the World Bank Open Data / World Development Indicators (WDI) API. It covers GDP, GDP per capita, GDP growth, consumer inflation, foreign direct investment, personal remittances, unemployment, total reserves, exports, and imports from 1960 to 2025 where observations are available.

## Dataset Details

- **Dataset ID**: `pakistan-macroeconomic-indicators`
- **Version**: `1.1.0`
- **Category**: `Economy and Finance`
- **Tags**: `economics`, `macroeconomics`, `gdp`, `inflation`, `trade`, `remittances`, `reserves`, `pakistan`, `time-series`
- **Language**: `English`
- **Geography**: `Pakistan (national aggregate)`
- **Time Period**: `1960 - 2025`
- **File Formats**: `CSV`
- **Records**: `600 observations across 10 indicators`
- **Update Frequency**: `Annual`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: World Bank Open Data - World Development Indicators (WDI)
- **Source URL**: https://data.worldbank.org/country/pakistan
- **Source Type**: Public open-data API (`https://api.worldbank.org/v2/country/PAK/indicator/...`)
- **Collection Method**: Programmatic download of per-indicator JSON responses for country `PAK`, filtered to non-null observations.
- **Collection Date**: July 4, 2026
- **Processing Pipeline**: Merged per-indicator API responses into a single long-format table (`indicator_code, indicator_name, year, value, unit`), dropped null values, added unit labels, sorted by indicator and year.
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
- Macroeconomic trend analysis and forecasting.
- Feature engineering for country-level economic, finance, development, and policy models.
- Teaching examples for long-format time-series analysis.

## Out-of-Scope Use

- Real-time financial trading or investment advice; values are annual national aggregates and may lag.
- Sub-national fiscal or economic analysis; values are national aggregates.
- Interpreting provisional or revised years without checking the latest World Bank metadata.

## Data Structure

Single CSV at `data/processed/macroeconomic_indicators.csv` in long format. One row represents one indicator-year observation.

Columns:
- `indicator_code`: World Bank WDI indicator code.
- `indicator_name`: World Bank indicator name.
- `year`: Gregorian calendar year.
- `value`: Numeric observation.
- `unit`: Curated unit label.

Indicators included:
- `BX.KLT.DINV.CD.WD`: Foreign direct investment, net inflows (BoP, current US$)
- `BX.TRF.PWKR.CD.DT`: Personal remittances, received (current US$)
- `FI.RES.TOTL.CD`: Total reserves (includes gold, current US$)
- `FP.CPI.TOTL.ZG`: Inflation, consumer prices (annual %)
- `NE.EXP.GNFS.CD`: Exports of goods and services (current US$)
- `NE.IMP.GNFS.CD`: Imports of goods and services (current US$)
- `NY.GDP.MKTP.CD`: GDP (current US$)
- `NY.GDP.MKTP.KD.ZG`: GDP growth (annual %)
- `NY.GDP.PCAP.CD`: GDP per capita (current US$)
- `SL.UEM.TOTL.ZS`: Unemployment, total (% of total labor force)

## Data Dictionary

See [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 100 / 100
- **Rating**: Excellent
- **Missing Values**: Null observations removed; coverage varies by indicator and year.
- **Duplicate Rows**: 0% (primary key: `indicator_code` + `year`).
- **Validation Status**: Passed CSV integrity validation.
- **Known Issues**: World Bank API calls for official exchange rate (`PA.NUS.FCRF`), current-account balance (`BN.CAB.XOKA.CD`), and external debt stocks (`DT.DOD.DECT.CD`) returned repeated gateway/time-out errors during the July 4, 2026 build and are not included in v1.1.0.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (aggregate national statistics, no personal data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None
- **Reviewer**: OpenDoc Data Stewardship Team
- **Review Date**: July 4, 2026

## Bias, Gaps, and Limitations

- National aggregates hide provincial, sectoral, urban/rural, and income-group differences.
- Some indicators are modelled estimates and may be revised by the World Bank.
- Indicator coverage is uneven: not every metric has observations back to 1960.
- Values are calendar-year WDI series and may not align with Pakistan fiscal-year reporting.

## Example Usage

```python
import pandas as pd

df = pd.read_csv("data/processed/macroeconomic_indicators.csv")

inflation = df[df["indicator_code"] == "FP.CPI.TOTL.ZG"]
print(inflation[["year", "value"]].tail(10))
```

## Citation

```text
World Bank, "World Development Indicators - Pakistan", curated as "Pakistan Macroeconomic Indicators" by OpenDoc Pakistan (OpenDoc), v1.1.0, 2026.
```
