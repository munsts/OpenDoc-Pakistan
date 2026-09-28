# Pakistan Taxpayer Heatmap and Regional Collections (FY 2020 - FY 2025)

## Summary

This dataset presents an authoritative, geospatial time series of revenue mobilization across Pakistan's **23 Federal Board of Revenue (FBR) field formations**—comprising Large Taxpayer Offices (LTOs), Corporate Tax Offices (CTOs), Medium Taxpayers Offices (MTOs), and Regional Tax Offices (RTOs)—spanning fiscal years 2020 through 2025 (138 formation-year observations).

Each record pairs financial performance metrics (Direct Taxes, Domestic/Import Sales Tax, Federal Excise Duty, Total Collections, and Active Taxpayer Filer populations) with precise **WGS84 geospatial coordinates (latitude and longitude)**, enabling direct rendering of spatial heatmaps, regional fiscal contribution cartograms, and geographical tax disparity analyses.

## Dataset Details

- **Dataset ID**: `pakistan-taxpayer-heatmap-and-collections`
- **Version**: `1.0.0`
- **Category**: `Taxation & Public Finance`
- **Tags**: `tax`, `taxpayers`, `fbr`, `revenue`, `heatmap`, `gis`, `income-tax`, `sales-tax`, `filers`, `atl`, `karachi`, `lahore`, `islamabad`, `peshawar`, `quetta`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan (23 Tax Formations across Sindh, Punjab, KPK, Balochistan, ICT)`
- **Time Period**: `FY 2019-20 to FY 2024-25`
- **File Formats**: `CSV`
- **Size**: `~17 KB`
- **Update Frequency**: `Annually (following FBR Year Book release)`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: Federal Board of Revenue (FBR), Government of Pakistan
- **Source URL**: https://www.fbr.gov.pk
- **Source Type**: Official Government Revenue Administration Year Books & Statistical Appendices
- **Collection Method**: Ingested and reconciled from official FBR Year Books (FY 2020 through FY 2025) and Active Taxpayer List (ATL) analytical reports.
- **Collection Date**: September 2026
- **Processing Pipeline**: Standardized administrative nomenclature, paired formations with city-centroid coordinates for GIS visualization, normalized collections across direct and indirect heads, and verified national total reconciliations.

## License

- **Original License**: Open Government Data License (OGDL) Pakistan
- **Repository License**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Redistribution**: Allowed

## Intended Use

Appropriate for:
- Geospatial choropleth and point-density heatmapping of tax generation across Pakistan.
- Fiscal federalism, revenue generation concentration, and provincial tax base research.
- Tracking the expansion of the Active Taxpayer List (ATL) filers post-digitization.
- Public finance policy research on direct versus indirect tax structures.

## Data Structure

The primary data file is located at `data/processed/taxpayer_heatmap_and_collections.csv`:

| Column | Type | Description |
| :--- | :--- | :--- |
| `formation_code` | string | Unique FBR code (`LTO_KHI`, `RTO_LHR`, `CTO_ISB`, etc.) |
| `formation_name` | string | Official title of the FBR tax office formation |
| `formation_type` | string | Office tier (`LTO`, `CTO`, `MTO`, `RTO`) |
| `principal_city` | string | City housing the tax office headquarters |
| `province` | string | Province or territory (Sindh, Punjab, KPK, Balochistan, ICT) |
| `latitude` | number | Decimal latitude (WGS84) for geospatial GIS mapping |
| `longitude` | number | Decimal longitude (WGS84) for geospatial GIS mapping |
| `fiscal_year` | integer | Fiscal year (e.g., 2024 for FY 2023-24) |
| `direct_tax_income_tax_pkr_billion` | number | Direct taxes collected (Income Tax, Super Tax) in PKR Billion |
| `sales_tax_pkr_billion` | number | Sales tax collected in PKR Billion |
| `federal_excise_duty_pkr_billion` | number | Federal Excise Duty (FED) in PKR Billion |
| `total_tax_collected_pkr_billion` | number | Total gross tax collection in PKR Billion |
| `share_of_national_tax_pct` | number | Percentage share of total national FBR tax revenue |
| `active_taxpayers_filers_count` | integer | Total active registered income tax filers |

## Key Insights from Regional Data

1. **Revenue Concentration in Karachi**: LTO Karachi, CTO Karachi, and MTO Karachi collectively contribute over **40% of Pakistan's total domestic tax revenue**, primarily driven by corporate headquarters, large financial institutions, import clearing, and multinational entities.
2. **Lahore & Upper Punjab Industrial Hub**: LTO Lahore, CTO Lahore, and RTOs (Lahore, Gujranwala, Sialkot, Faisalabad) represent the industrial manufacturing backbone, accounting for approximately **30% of total tax collection**.
3. **Surge in Active Filers**: Registered active taxpayer filers expanded dramatically from ~2.45 million in 2020 to over **6.85 million in 2025**, driven by heightened withholding tax penalties on non-filers and automated banking compliance systems.

## Quality Report

- **Quality Score**: 100 / 100
- **Rating**: Excellent
- **Missing Values**: 0%
- **Duplicate Rows**: 0%
- **Validation Status**: Passed (Schema validated, UTF-8 encoded)

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (Official institutional-level and regional aggregate statistics, no individual taxpayer data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No

## Example Usage: Interactive Heatmap with Folium

```python
import pandas as pd
import folium
from folium.plugins import HeatMap

# Load dataset
df = pd.read_csv("data/processed/taxpayer_heatmap_and_collections.csv")

# Filter for latest fiscal year
df_latest = df[df["fiscal_year"] == 2025]

# Initialize map centered on Pakistan
pakistan_map = folium.Map(location=[30.3753, 69.3451], zoom_start=6)

# Generate HeatMap data: [lat, lon, weight]
heat_data = [[row["latitude"], row["longitude"], row["total_tax_collected_pkr_billion"]] for _, row in df_latest.iterrows()]
HeatMap(heat_data, radius=25, blur=15, max_zoom=10).add_to(pakistan_map)

# Add markers for top 5 tax collecting formations
for _, row in df_latest.sort_values(by="total_tax_collected_pkr_billion", ascending=False).head(5).iterrows():
    folium.Marker(
        location=[row["latitude"], row["longitude"]],
        popup=f"{row['formation_name']}: PKR {row['total_tax_collected_pkr_billion']:.1f}B ({row['share_of_national_tax_pct']}%)",
        icon=folium.Icon(color="red", icon="info-sign")
    ).add_to(pakistan_map)

pakistan_map.save("taxpayer_heatmap_pakistan.html")
print("Saved interactive heatmap to taxpayer_heatmap_pakistan.html")
```

## Citation

```text
Federal Board of Revenue (FBR), "Pakistan Taxpayer Heatmap and Regional Collections (FY 2020 - FY 2025)", curated and structured by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
