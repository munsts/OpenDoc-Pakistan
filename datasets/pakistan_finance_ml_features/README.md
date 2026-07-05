# Pakistan Finance ML Features

## Summary

This dataset contains separate machine-learning feature tables for Pakistan finance. It is not mixed with the RAG corpus. Tables include monthly inflation/macro features, weekly SPI item-city price features, government securities yield features, and interest corridor facility-usage features.

## Dataset Details

- **Dataset ID**: `pakistan-finance-ml-features`
- **Version**: `0.1.0`
- **Category**: `Economy and Finance`
- **Tags**: `machine-learning`, `forecasting`, `features`, `inflation`, `spi`, `bonds`, `yields`, `interest-rates`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan`
- **File Formats**: `CSV`
- **Records**: `35,085 feature rows`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

Features are derived from the separate curated packages:

- `pakistan_inflation_and_prices`
- `pakistan_government_securities_auctions`
- `pakistan_interest_rate_corridor`
- `pakistan_macroeconomic_indicators`

No RAG chunks or QA text are included in this package.

## License

- **Original License**: Mixed official public website sources; explicit open redistribution licenses not found for PBS/SBP, World Bank WDI is CC-BY.
- **Repository License**: `LicenseRef-PBS-Public-Website`, `LicenseRef-SBP-Public-Website`, and World Bank WDI attribution.
- **Attribution Required**: Yes, cite the underlying official sources.

## Files

- `monthly_macro_inflation_features.csv`: monthly CPI/SPI/WPI features, WDI annual macro joins, lags, rolling averages, and next-month targets.
- `weekly_spi_price_features.csv`: weekly item-city average prices with lag, rolling, next-week price, and direction targets.
- `government_securities_yield_features.csv`: T-bill/PIB auction yield features with lag and next-auction targets.
- `interest_corridor_daily_features.csv`: SBP corridor facility usage features with lag, rolling, and next-observation targets.

## ML Notes

- Features are time ordered.
- Target columns are explicitly prefixed with `target_`.
- Splits are chronological, not random.
- Lag/rolling features use prior observations only.
- Blank targets at the end of a group are expected where no future observation exists.

## Quality Report

- **Duplicate Primary Keys**: 0
- **Blank Primary Keys**: 0
- **PII Scan**: 0 email/phone regex hits.
- **Known Limitation**: Some features inherit source frequency differences: monthly inflation, weekly prices, auction events, and daily/operation corridor records are separate tables by design.

## Intended Use

Appropriate for:
- Inflation direction and level forecasting.
- SPI item/city price anomaly detection.
- Auction yield movement modeling.
- Liquidity facility usage modeling.

Out of scope:
- Retrieval/citation QA; use `pakistan_finance_rag_corpus`.
- Trading or investment advice.

## Citation

```text
Pakistan Bureau of Statistics, State Bank of Pakistan, and World Bank WDI sources, curated as "Pakistan Finance ML Features" by OpenDoc Pakistan (OpenDoc), v0.1.0, 2026.
```
