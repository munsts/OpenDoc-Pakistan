# Pakistan Top Corporate Financials, Taxation, and Effective Tax Rates (2020-2024)

## Summary

This dataset compiles extensive multi-year financial statements analysis and corporate tax contributions for **64 leading listed corporate entities** across 15 major industrial sectors on the **Pakistan Stock Exchange (PSX)** over fiscal years 2020 through 2024 (310 entity-year observations). It provides granular metrics on gross revenue turnover, profit before tax (PBT), provision for taxation / taxes paid, profit after tax (PAT), effective tax rates (ETR), balance sheet asset valuations, and sectoral tax burdens. It also tracks the impact of Section 4C Super Tax enacted in recent fiscal years.

## Dataset Details

- **Dataset ID**: `pakistan-corporate-financials-and-taxes`
- **Version**: `1.0.0`
- **Category**: `Corporate Finance & Taxation`
- **Tags**: `corporate`, `financials`, `taxation`, `effective-tax-rate`, `super-tax`, `revenue`, `psx`, `fbr`, `sbp`, `pakistan`, `banking`, `energy`, `cement`, `textile`
- **Language**: `English`
- **Geography**: `Pakistan (National Corporate Sector)`
- **Time Period**: `2020 - 2024`
- **File Formats**: `CSV`
- **Size**: `~33 KB` (Entity records) + `~6 KB` (Sector summary)
- **Update Frequency**: `Annually`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: State Bank of Pakistan (SBP) Financial Statements Analysis (FSA), Annual Audited Financial Reports, and Pakistan Stock Exchange (PSX) Disclosures
- **Source URL**: https://www.sbp.org.pk / https://dps.psx.com.pk
- **Source Type**: Official Financial Regulator Publications & Audited Corporate Disclosures
- **Collection Method**: Systematic extraction and normalization from audited annual financial statements and SBP non-financial company analytical datasets.
- **Collection Date**: September 2026
- **Processing Pipeline**: Standardized fiscal year accounting periods, normalized pre-tax and post-tax line items, calculated analytical Effective Tax Rates (`ETR = (Tax Expense / PBT) * 100`), flagged statutory Super Tax applicability, and produced sector-level aggregated summaries.

## License

- **Repository License**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Redistribution**: Allowed

## Intended Use

Appropriate for:
- Corporate tax incidence and effective tax rate (ETR) disparity studies across sectors.
- Fiscal policy modeling assessing the macroeconomic impact of Super Tax (Section 4C) and turnover tax regimes.
- Sectoral profitability, revenue concentration, and corporate balance sheet health analysis.
- Benchmarking corporate contributions to the national exchequer against FBR total direct tax receipts.

## Data Structure

### 1. Primary Entity Records (`data/processed/corporate_financials_and_taxes.csv`)

| Column | Type | Description |
| :--- | :--- | :--- |
| `symbol` | string | PSX ticker symbol (e.g. `OGDC`, `LUCK`, `SYS`, `FFC`, `HBL`) |
| `company_name` | string | Full legal name of the registered entity |
| `sector` | string | Industrial sector (Commercial Banks, Fertilizer, Oil & Gas, etc.) |
| `market_cap_category` | string | Market capitalization classification (`Large Cap`, `Mid Cap`) |
| `fiscal_year` | integer | Fiscal accounting year (2020–2024) |
| `revenue_pkr_million` | number | Gross revenue or turnover / markup earned for banks (PKR Million) |
| `profit_before_tax_pkr_million` | number | Pre-tax profit or loss (PKR Million) |
| `tax_expense_pkr_million` | number | Total tax provision including corporate tax and Super Tax (PKR Million) |
| `profit_after_tax_pkr_million` | number | Net profit after tax (PKR Million) |
| `effective_tax_rate_pct` | number | Effective tax rate percentage (`tax / PBT * 100`) |
| `total_assets_pkr_million` | number | Total balance sheet asset size (PKR Million) |
| `super_tax_applicable` | string | `true` if Section 4C Super Tax applied in fiscal year |

### 2. Sectoral Summary (`data/processed/sectoral_tax_and_revenue_summary.csv`)

Aggregates total corporate turnover, cumulative taxes contributed, pre-tax profits, and sector-weighted effective tax rates across 15 industries annually.

## Sector Tax Profile Insights

1. **Commercial Banks**: Highest effective tax burden in Pakistan (~48% to 55%), reflecting statutory corporate tax (39%) plus 10% Super Tax and ADR shortfall surcharges.
2. **Oil & Gas Exploration**: High gross tax contributors (~25% to 35% ETR) with immense revenue generation (e.g., OGDC alone generating over PKR 460 Billion turnover).
3. **Fertilizer & Cement**: Heavy domestic industrial contributors with effective tax rates scaling to 35–42% following Super Tax enactments.
4. **Technology & Software**: Beneficiaries of export incentive regimes with effective tax rates ranging between 4% and 9%.
5. **Textile Exporters**: Subject to presumptive / Final Tax Regimes (FTR) based on 1–2% turnover withholding.

## Quality Report

- **Quality Score**: 100 / 100
- **Rating**: Excellent
- **Missing Values**: 0%
- **Duplicate Rows**: 0%
- **Validation Status**: Passed (Schema validated, UTF-8 encoded)

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (Publicly listed companies, publicly audited financial statements)
- **Personal Data Present**: No
- **Sensitive Data Present**: No

## Example Usage

```python
import pandas as pd

# Load dataset
df = pd.read_csv("data/processed/corporate_financials_and_taxes.csv")

# 1. Top 5 corporate taxpayers in 2024
top_taxpayers_2024 = df[df["fiscal_year"] == 2024].sort_values(
    by="tax_expense_pkr_million", ascending=False
)[["symbol", "company_name", "sector", "tax_expense_pkr_million", "effective_tax_rate_pct"]].head(5)
print("Top 5 Listed Corporate Taxpayers (2024):")
print(top_taxpayers_2024.to_string(index=False))

# 2. Sectoral Effective Tax Rates for 2024
sector_summary = pd.read_csv("data/processed/sectoral_tax_and_revenue_summary.csv")
s2024 = sector_summary[sector_summary["fiscal_year"] == 2024].sort_values(
    by="total_tax_paid_pkr_billion", ascending=False
)
print("\nSectoral Corporate Tax Contributions (2024):")
print(s2024[["sector", "total_revenue_pkr_billion", "total_tax_paid_pkr_billion", "sector_effective_tax_rate_pct"]].to_string(index=False))
```

## Citation

```text
State Bank of Pakistan (SBP) / Pakistan Stock Exchange (PSX), "Pakistan Top Corporate Financials, Taxation, and Effective Tax Rates (2020-2024)", curated by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
