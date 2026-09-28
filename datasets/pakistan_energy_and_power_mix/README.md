# Pakistan Energy and Power Generation Mix (1990-2024)

## Summary

This dataset delivers an authoritative, multi-decade time series (1990–2024) tracking Pakistan's electric power system evolution. It captures the nation's changing generation fuel mix—including hydroelectric, natural gas, furnace oil/diesel, coal, nuclear, and non-hydro renewables (solar, wind, bagasse)—alongside national, rural, and urban electricity access rates, transmission and distribution losses, and per-capita electrical power consumption.

## Dataset Details

- **Dataset ID**: `pakistan-energy-and-power-mix`
- **Version**: `1.0.0`
- **Category**: `Energy & Infrastructure`
- **Tags**: `energy`, `power`, `electricity`, `generation`, `hydel`, `coal`, `gas`, `nuclear`, `renewables`, `nepra`, `pakistan`, `time-series`
- **Language**: `English`
- **Geography**: `Pakistan (National Grid & Distribution)`
- **Time Period**: `1990 - 2024`
- **File Formats**: `CSV`
- **Size**: `~43 KB`
- **Update Frequency**: `Annually`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: World Bank Open Data / World Development Indicators (WDI), National Electric Power Regulatory Authority (NEPRA) State of Industry Reports, and Hydrocarbon Development Institute of Pakistan (HDIP)
- **Source URL**: https://data.worldbank.org / https://nepra.org.pk
- **Source Type**: Official Multilateral API & National Sector Regulators
- **Collection Method**: Systematic ingestion via the World Bank Indicators API and regulatory annual reports.
- **Collection Date**: September 2026
- **Processing Pipeline**: Long-format tabular standardization, precision rounding, unit normalization, and integrity verification.

## License

- **Original License**: Creative Commons Attribution 4.0 International (CC BY 4.0) via World Bank Open Data Terms
- **Repository License**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Redistribution**: Allowed

## Intended Use

Appropriate for:
- Energy transition and decarbonization policy modeling.
- Economic research on power circular debt and fuel-cost pass-through implications.
- Forecasting electricity demand, grid penetration, and renewable capacity growth.
- Comparative infrastructure analysis across South Asia.

## Out-of-Scope Use

Prohibited or discouraged uses:
- Real-time intra-day dispatch scheduling (represents annual aggregated operational data).
- Feeder-level fault localization.

## Data Structure

The primary data file is located at `data/processed/energy_and_power_mix.csv` in tidy long format:

| Column | Type | Description |
| :--- | :--- | :--- |
| `indicator_code` | string | World Bank WDI code for the energy metric |
| `indicator_name` | string | Full human-readable name of the indicator |
| `year` | integer | Observation year (1990 to 2024) |
| `value` | number | Recorded numeric metric value |
| `unit` | string | Standardized measurement unit |

### Key Indicators Tracked

- `EG.ELC.ACCS.ZS`: Access to electricity (% of population)
- `EG.ELC.ACCS.RU.ZS`: Access to electricity, rural (% of rural population)
- `EG.ELC.ACCS.UR.ZS`: Access to electricity, urban (% of urban population)
- `EG.ELC.HYRO.ZS`: Electricity production from hydroelectric sources (% of total)
- `EG.ELC.NGAS.ZS`: Electricity production from natural gas sources (% of total)
- `EG.ELC.PETR.ZS`: Electricity production from oil sources (% of total)
- `EG.ELC.COAL.ZS`: Electricity production from coal sources (% of total)
- `EG.ELC.NUCL.ZS`: Electricity production from nuclear sources (% of total)
- `EG.ELC.RNWX.ZS`: Electricity production from renewable sources, excluding hydro (% of total)
- `EG.ELC.LOSS.ZS`: Electric power transmission and distribution losses (% of output)
- `EG.USE.ELEC.KH.PC`: Electric power consumption (kWh per capita)
- `EG.FEC.RNEW.ZS`: Renewable energy consumption (% of total final energy consumption)

## Quality Report

- **Quality Score**: 100 / 100
- **Rating**: Excellent
- **Missing Values**: 0% across all 383 records
- **Duplicate Rows**: 0%
- **Validation Status**: Passed (Schema validated, UTF-8 encoded)

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (National-level infrastructure aggregate statistics)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Reviewer**: OpenDoc Compliance Board

## Example Usage

```python
import pandas as pd

# Load dataset
df = pd.read_csv("data/processed/energy_and_power_mix.csv")

# Filter generation sources for 2020 vs 2023
sources = [
    "EG.ELC.HYRO.ZS", "EG.ELC.NGAS.ZS", "EG.ELC.PETR.ZS",
    "EG.ELC.COAL.ZS", "EG.ELC.NUCL.ZS", "EG.ELC.RNWX.ZS"
]
gen_df = df[df["indicator_code"].isin(sources)]
pivot = gen_df.pivot(index="year", columns="indicator_name", values="value")
print("Power Generation Mix Evolution (Recent Years):")
print(pivot.tail(5))
```

## Citation

```text
World Bank / NEPRA / HDIP, "Pakistan Energy and Power Generation Mix (1990-2024)", curated by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
