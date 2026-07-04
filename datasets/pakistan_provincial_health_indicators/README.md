# Pakistan Provincial Child Health Indicators (PDHS 2017-18)

## Summary

Province-level child health indicators for Pakistan's four main provinces (Punjab, Sindh, Khyber Pakhtunkhwa, Balochistan), covering child **nutrition** (stunting, wasting, underweight) and childhood **immunization** coverage (BCG, measles, all-basic vaccinations, no vaccinations). Sourced from the Pakistan Demographic and Health Survey (PDHS) 2017-18. This dataset fills the sub-national gap left by national-aggregate series such as `pakistan_health_indicators` and `pakistan_disease_surveillance`, exposing the large inter-provincial disparities those national figures hide.

## Dataset Details

- **Dataset ID**: `pakistan-provincial-health-indicators`
- **Version**: `1.0.0`
- **Category**: `Health`
- **Tags**: `nutrition`, `stunting`, `wasting`, `immunization`, `vaccination`, `provincial`, `pdhs`, `children`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan (Punjab, Sindh, Khyber Pakhtunkhwa, Balochistan)`
- **Time Period**: `2017-2018 (PDHS reference)`
- **File Formats**: `CSV`
- **Records**: `28 observations (4 provinces x 7 indicators)`
- **Update Frequency**: `Per DHS round (~5 years)`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: Pakistan Demographic and Health Survey (PDHS) 2017-18, Key Indicators Report
- **Source URL**: https://dhsprogram.com/pubs/pdf/FR354/FR354.pdf
- **Source Type**: National household survey (NIPS / National Institute of Population Studies with ICF, The DHS Program)
- **Collection Method**: Values extracted from the PDHS Key Indicators PDF via automated PDF parsing (firecrawl `parse`), then transcribed from Table 11 (vaccinations, children 12-23 months) and Table 13 (nutritional status of children under 5). Stunting/wasting/underweight are the percentage of children below -2 SD (height-for-age, weight-for-height, weight-for-age respectively).
- **Collection Date**: July 2026
- **Processing Pipeline**: Parsed PDF -> located province rows in Tables 11 & 13 -> mapped labelled columns -> long-format CSV (`province, indicator_code, indicator_name, year, value, unit`).
- **Raw Data Availability**: Public PDHS report; full microdata available via the DHS Program (registration required).

## License

- **Original License**: The DHS Program permits use of published report data with attribution.
- **Repository License**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Restrictions**: Must credit NIPS, ICF / The DHS Program, and OpenDoc Pakistan.

## Intended Use

Appropriate for:
- Comparing child nutrition and immunization outcomes across provinces.
- Highlighting provincial disparities for policy, advocacy, and dashboards.
- Combining with national series for multi-scale analysis.

## Out-of-Scope Use

- District-level analysis (data is province-level).
- Trend analysis across survey rounds (this release contains only PDHS 2017-18).
- Clinical or individual-level decisions.

## Data Structure

Single CSV at `data/processed/provincial_health_indicators.csv` in long format. One row per province per indicator.

Indicators: `stunting`, `wasting`, `underweight` (nutrition); `bcg`, `measles`, `basic_vaccination`, `no_vaccination` (immunization).

## Data Dictionary

See [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 100 / 100
- **Rating**: Excellent
- **Records**: 28 (4 provinces x 7 indicators)
- **Duplicate Rows**: 0% (primary key: `province` + `indicator_code`)
- **Validation Status**: Passed Frictionless tabular-data-resource schema.
- **Known Issues**: Only the four main provinces are included; ICT Islamabad, FATA, AJK, and Gilgit-Baltistan rows were excluded because the parsed PDF rows for those regions showed column-alignment artefacts and were not reliably verifiable.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (aggregate survey estimates; no personal data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None

## Bias, Gaps, and Limitations

- Survey estimates carry sampling error; small-sample regions were excluded for reliability.
- Province aggregates still mask district and urban/rural disparities.
- Values reflect 2017-18; coverage and nutrition status may have shifted since.

## Example Usage

```python
import pandas as pd

df = pd.read_csv("data/processed/provincial_health_indicators.csv")

# Stunting by province
print(df[df["indicator_code"] == "stunting"][["province", "value"]])
```

## Citation

```text
National Institute of Population Studies (NIPS) and ICF, "Pakistan Demographic and Health Survey 2017-18", curated as "Pakistan Provincial Child Health Indicators" by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
