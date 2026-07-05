# Pakistan Government Securities Auctions

## Summary

This dataset packages official State Bank of Pakistan (SBP) auction history for Market Treasury Bills and Pakistan Investment Bonds. It includes detailed auction amounts, T-bill cut-off prices, weighted-average yields for T-bills and PIBs, and outstanding fixed-rate PIB securities.

## Dataset Details

- **Dataset ID**: `pakistan-government-securities-auctions`
- **Version**: `0.1.0`
- **Category**: `Economy and Finance`
- **Tags**: `finance`, `government-securities`, `treasury-bills`, `bonds`, `yields`, `auctions`, `pakistan`, `sbp`
- **Language**: `English`
- **Geography**: `Pakistan`
- **Time Period**: `1998 - 2026`
- **File Formats**: `CSV`
- **Records**: `3,635 rows across 5 CSV resources`
- **Update Frequency**: `Monthly or as SBP auction files are updated`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: State Bank of Pakistan (SBP), Economic Data
- **Source URL**: https://www.sbp.org.pk/economic-data
- **Source Files**:
  - `https://www.sbp.org.pk/assets/document/tb.xlsx`
  - `https://www.sbp.org.pk/assets/document/Pakinvestbonds.xlsx`
- **Source Type**: Official central bank publication
- **Collection Date**: July 4, 2026
- **Processing Pipeline**: Downloaded official SBP Excel workbooks, parsed workbook XML locally, normalized old and new workbook tabs into CSV resources, converted Excel serial dates to ISO dates, removed non-numeric rejected/no-bid yield cells.
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
- Government securities auction analysis.
- Yield-curve and money-market research.
- Fixed-income ML feature engineering.
- Backtesting macro-financial indicators at auction frequency.

## Out-of-Scope Use

- Real-time trading; this is historical official auction data.
- Legal or investment advice.
- Redistribution as open data without confirming SBP terms.

## Data Structure

Resources:
- `tbill_auction_results.csv`: detailed Market Treasury Bill auction bids and accepted amounts.
- `tbill_weighted_average_yields.csv`: long-format T-bill weighted-average yields by auction and tenor.
- `pib_auction_results.csv`: detailed Pakistan Investment Bond auction bids and accepted amounts.
- `pib_weighted_average_yields.csv`: long-format PIB weighted-average yields by auction and tenor.
- `pib_outstanding_securities.csv`: outstanding fixed-rate PIB securities and face values.

## Data Dictionary

See [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 95 / 100
- **Validation Status**: CSV validation passed for all resources.
- **Missing Values**: Yield resources have no missing values. Detailed auction resources preserve blanks where a source workbook field was not applicable, such as rejected/no-bid tenors or missing ISINs in older rows.
- **Duplicate Rows**: 0 duplicate rows in generated resources.
- **Known Issues**: PIB detailed auction workbook does not expose yield fields in the new-format sheet, so PIB weighted-average yields are provided from the old-format sheet.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (aggregate market statistics, no personal data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None

## Bias, Gaps, and Limitations

- SBP workbook formats changed over time; old and new formats are preserved as separate normalized resources.
- Rejected/no-bid T-bill cells are excluded from yield rows.
- The dataset reflects official auction publications, not secondary-market prices.

## Example Usage

```python
import pandas as pd

yields = pd.read_csv("data/processed/tbill_weighted_average_yields.csv")
latest = yields.sort_values("auction_date").tail(20)
print(latest[["auction_date", "tenor", "weighted_average_yield_pct"]])
```

## Citation

```text
State Bank of Pakistan, "Auction Result of Market Treasury Bills" and "Pakistan Investment Bonds Auction Results", curated as "Pakistan Government Securities Auctions" by OpenDoc Pakistan (OpenDoc), v0.1.0, 2026.
```
