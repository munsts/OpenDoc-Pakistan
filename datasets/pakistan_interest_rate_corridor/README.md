# Pakistan Interest Rate Corridor Facility Usage

## Summary

This dataset contains official State Bank of Pakistan history for access to overnight repo and reverse repo facilities. It tracks the SBP corridor ceiling and floor facility amounts and the number of participating institutions by date.

## Dataset Details

- **Dataset ID**: `pakistan-interest-rate-corridor`
- **Version**: `0.1.0`
- **Category**: `Economy and Finance`
- **Tags**: `finance`, `interest-rates`, `policy-rate`, `repo`, `reverse-repo`, `monetary-policy`, `pakistan`, `sbp`
- **Language**: `English`
- **Geography**: `Pakistan`
- **Time Period**: `2009 - 2026`
- **File Formats**: `CSV`
- **Records**: `2,231 observations`
- **Update Frequency**: `Occasional; latest source file dated July 3, 2026`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: State Bank of Pakistan (SBP), Economic Data
- **Source URL**: https://www.sbp.org.pk/economic-data
- **Source File**: `https://www.sbp.org.pk/assets/document/IR-Corridor-Hist.xls`
- **Source Type**: Official central bank publication
- **Collection Date**: July 4, 2026
- **Processing Pipeline**: Downloaded the official SBP legacy Excel workbook, parsed the `Corridor` sheet, converted Excel serial dates to ISO dates, and normalized facility amounts/institution counts into CSV.
- **Raw Data Availability**: Public on SBP Economic Data pages.

## License

- **Original License**: SBP public website data; explicit open redistribution license not found.
- **Repository License**: `LicenseRef-SBP-Public-Website`
- **Attribution Required**: Yes, cite the State Bank of Pakistan.
- **Commercial Use**: No explicit restriction found in the source page reviewed.
- **Redistribution**: No explicit restriction found in the source page reviewed; use with attribution to SBP.
- **Restriction**: Do not label as CC-BY or public domain unless SBP publishes explicit open-license terms.

## Intended Use

Appropriate for:
- Monetary-policy and liquidity-condition analysis.
- Interest-rate corridor monitoring.
- Macro-financial feature engineering.

## Out-of-Scope Use

- Real-time trading or investment advice.
- Open redistribution before confirming SBP licensing.

## Data Structure

Single CSV at `data/processed/interest_rate_corridor.csv`.

Columns:
- `date`: Observation date.
- `ceiling_amount_million_pkr`: Overnight repo ceiling facility amount.
- `ceiling_institutions`: Number of institutions using the ceiling facility.
- `floor_amount_million_pkr`: Reverse repo floor facility amount.
- `floor_institutions`: Number of institutions using the floor facility.

## Data Dictionary

See [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 95 / 100
- **Validation Status**: CSV validation passed.
- **Missing Values**: 0%.
- **Duplicate Rows**: 0%.
- **Known Issues**: The source records facility usage, not the policy-rate level itself.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (aggregate facility usage, no personal data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None

## Bias, Gaps, and Limitations

- Facility usage is a liquidity-operation measure and should not be interpreted as a complete policy-rate series.
- The original workbook is a legacy `.xls` file and may change format in future SBP updates.

## Example Usage

```python
import pandas as pd

df = pd.read_csv("data/processed/interest_rate_corridor.csv")
df["date"] = pd.to_datetime(df["date"])
print(df.tail())
```

## Citation

```text
State Bank of Pakistan, "Access to Overnight Repo/Reverse Repo Facilities-History", curated as "Pakistan Interest Rate Corridor Facility Usage" by OpenDoc Pakistan (OpenDoc), v0.1.0, 2026.
```
