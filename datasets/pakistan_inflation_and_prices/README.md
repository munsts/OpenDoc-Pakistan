# Pakistan Inflation and SPI Prices

## Summary

This dataset contains official Pakistan Bureau of Statistics (PBS) inflation and price data, including historical CPI/WPI index values, historical year-on-year inflation rates, latest monthly inflation-rate tables, weekly Sensitive Price Indicator (SPI) city-item prices, weekly SPI expenditure-group summaries, weekly item-level price-change tables, and monthly SPI city-item average prices.

## Dataset Details

- **Dataset ID**: `pakistan-inflation-and-prices`
- **Version**: `0.1.0`
- **Category**: `Economy and Finance`
- **Tags**: `finance`, `inflation`, `cpi`, `spi`, `wpi`, `prices`, `pakistan`, `pbs`
- **Language**: `English`
- **Geography**: `Pakistan`
- **Time Period**: `2017-07 - 2026-07`
- **File Formats**: `CSV`
- **Records**: `106,593 parsed data observations plus 83 source-inventory records`
- **Update Frequency**: `Weekly/monthly at source`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: Pakistan Bureau of Statistics (PBS), Price Statistics
- **Source URL**: https://www.pbs.gov.pk/price-statistics/
- **Primary Source Files**:
  - `https://www.pbs.gov.pk/wp-content/uploads/2020/07/indices.pdf`
  - `https://www.pbs.gov.pk/wp-content/uploads/2020/07/Monthly-Review-June-2026.pdf`
  - PBS weekly SPI Excel annex/report files linked from the Price Statistics page
  - PBS monthly SPI prices Excel annex files linked from the Price Statistics page
- **Source Type**: Official national statistical office publication
- **Collection Date**: July 5, 2026
- **Processing Pipeline**: Downloaded official PBS source files, parsed embedded-text PDF tables with `pypdf`, parsed Excel workbooks through Open XML, normalized repeated city/item workbook blocks into long CSVs, corrected one malformed PBS link path (`wp-contet` to `wp-content`), and wrote source-inventory files for auditability.
- **OCR Decision**: OCR was checked but not used. The PBS PDFs sampled have extractable text layers, and the largest SPI city/item tables are available as Excel. OCR would have reduced structural reliability for this package.
- **Raw Data Availability**: Public on the PBS Price Statistics page.

## License

- **Original License**: PBS public website data; explicit open redistribution license not found.
- **Repository License**: `LicenseRef-PBS-Public-Website`
- **Attribution Required**: Yes, cite Pakistan Bureau of Statistics.
- **Commercial Use**: No explicit restriction found in the source page reviewed.
- **Redistribution**: No explicit restriction found in the source page reviewed; use with attribution to PBS.
- **Restriction**: Do not label as CC-BY or public domain unless PBS publishes explicit open-license terms.

## Data Structure

CSV files are in `data/processed/`.

- `price_indices_historical.csv`: monthly CPI/WPI index values from `indices.pdf`, 2017-07 to 2025-01.
- `inflation_yoy_historical.csv`: monthly historical year-on-year CPI/WPI inflation rates from `indices.pdf`, 2017-07 to 2025-01.
- `monthly_inflation_rates_latest.csv`: PBS latest review Table 1.a monthly inflation rates, 2024-09 to 2026-06.
- `weekly_spi_city_item_prices.csv`: weekly SPI essential-item min/avg/max prices by city, 2025-10-23 to 2026-07-02.
- `weekly_spi_summary.csv`: weekly SPI by expenditure group/quintile and combined, 2025-10-23 to 2026-07-02.
- `weekly_spi_item_changes.csv`: weekly item-level SPI price changes, weights, and impact, 2025-10-23 to 2026-07-02.
- `monthly_spi_city_item_prices.csv`: monthly city-item average prices for SPI items and non-index essential items, 2025-07 to 2026-06.
- `source_inventory_weekly.csv`: weekly source-file inventory and parsed row counts.
- `source_inventory_monthly.csv`: monthly source-file inventory and parsed row counts.

## Data Dictionary

See [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 94 / 100
- **Validation Status**: CSV validation passed.
- **Duplicate Keys**: 0 duplicate primary keys in parsed tables.
- **Source Parse Errors**: 0 after correcting the malformed PBS path typo.
- **Missing Values**: Missing and not-available price cells are represented through `availability_status`.
- **Known Issues**: Some PBS weekly annex cells report `0` for unavailable city/item prices. These are not treated as real prices; `price_pkr`/`average_price_pkr` is blank and `availability_status` is `reported_zero`.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (aggregate official statistics, no personal data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None

## Bias, Gaps, and Limitations

- The `indices.pdf` historical archive currently parses through January 2025; the latest monthly review extends high-level inflation rates through June 2026.
- Weekly Excel sources currently available with complete workbook structure cover October 23, 2025 through July 2, 2026.
- Item-level prices are official published observations and should be interpreted with PBS collection methodology.
- Source terms do not state an explicit open-data license.

## Example Usage

```python
import pandas as pd

weekly = pd.read_csv("data/processed/weekly_spi_city_item_prices.csv")
weekly["week_end_date"] = pd.to_datetime(weekly["week_end_date"])
avg_wheat = weekly[
    (weekly["item_description"] == "Wheat Flour Bag")
    & (weekly["price_type"] == "avg")
    & (weekly["availability_status"] == "reported")
]
print(avg_wheat.tail())
```

## Citation

```text
Pakistan Bureau of Statistics, "Price Statistics", curated as "Pakistan Inflation and SPI Prices" by OpenDoc Pakistan (OpenDoc), v0.1.0, 2026.
```
