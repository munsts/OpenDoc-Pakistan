# Pakistan 2023 Digital Census: District Demographics and Housing

## Summary

This dataset compiles complete district-level demographic, spatial, and socioeconomic metrics from Pakistan's **7th Population and Housing Census (2023)**—the country's first-ever digital census conducted by the **Pakistan Bureau of Statistics (PBS)**. It covers all 152 administrative districts across Punjab, Sindh, Khyber Pakhtunkhwa, Balochistan, and the Islamabad Capital Territory (ICT), incorporating 2023 populations, intercensal historical totals (2017 and 1998 censuses), geographic areas, population densities, and district literacy rates.

## Dataset Details

- **Dataset ID**: `pakistan-census-2023-districts`
- **Version**: `1.0.0`
- **Category**: `Demographics & Governance`
- **Tags**: `census`, `demographics`, `population`, `districts`, `provinces`, `density`, `literacy`, `pakistan`, `pbs`
- **Language**: `English`
- **Geography**: `Pakistan (Punjab, Sindh, Khyber Pakhtunkhwa, Balochistan, Islamabad Capital Territory)`
- **Time Period**: `2023 (with historical comparison to 2017, 1998)`
- **File Formats**: `CSV`
- **Size**: `~12 KB`
- **Update Frequency**: `Decennial (Census Cycles)`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: Pakistan Bureau of Statistics (PBS), Government of Pakistan
- **Source URL**: https://www.pbs.gov.pk
- **Source Type**: Official National Census Reports & Publications
- **Collection Method**: 7th Population and Housing Census 2023 enumeration tables, unanimously approved by the Council of Common Interests (CCI) on August 5, 2023.
- **Collection Date**: March–May 2023 (Final results gazetted August 2023)
- **Processing Pipeline**: Standardized administrative nomenclature, normalized numerical formats, validated geographic hierarchies against provincial gazettes, and cross-referenced historical census series.

## License

- **Original License**: Open Government Data License (OGDL) Pakistan
- **Repository License**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Redistribution**: Allowed
- **Restrictions**: Must credit Pakistan Bureau of Statistics (PBS) and OpenDoc Pakistan.

## Intended Use

Appropriate for:
- Regional planning, resource allocation, and delimitation analysis.
- Demographic modeling, urbanization trends, and population density mapping.
- Spatial equity research correlating educational infrastructure with population pressures.
- Academic, economic, and policy studies on provincial development disparities.

## Out-of-Scope Use

Prohibited or discouraged uses:
- Micro-level or individual tracking (all records represent aggregated district units).
- Extrapolation to sub-tehsil or block levels without localized enumeration data.

## Data Structure

The primary data file is located at `data/processed/census_2023_districts.csv`:

| Column | Type | Description |
| :--- | :--- | :--- |
| `district` | string | Official administrative name of the district |
| `province` | string | Province or territory (Punjab, Sindh, KPK, Balochistan, ICT) |
| `division` | string | Administrative division containing the district |
| `headquarters` | string | District administrative headquarters town/city |
| `area_sq_km` | number | Total geographical area in square kilometers |
| `population_2023` | integer | Total enumerated population in the 2023 Digital Census |
| `population_2017` | integer | Total enumerated population in the 2017 Census (nullable for newly formed districts) |
| `population_1998` | integer | Total enumerated population in the 1998 Census (nullable) |
| `population_density_per_sq_km` | number | Calculated population density per square kilometer (2023) |
| `literacy_rate_pct` | number | Overall literacy rate percentage of population aged 10+ (2023) |

## Quality Report

- **Quality Score**: 100 / 100
- **Rating**: Excellent
- **Missing Values**: 0% in primary identifiers (`district`, `province`, `division`, `population_2023`)
- **Duplicate Rows**: 0%
- **Validation Status**: Passed (Schema validated, UTF-8 encoded)
- **Known Limitations**: Certain newly delineated districts established after 2017 or 1998 (e.g., in newly created administrative divisions) have null historical figures as their territories were previously counted within parent districts.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (Completely aggregated public statistics, no personally identifiable information)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Reviewer**: OpenDoc Compliance Board

## Example Usage

```python
import pandas as pd

# Load dataset
df = pd.read_csv("data/processed/census_2023_districts.csv")
print(f"Total districts: {len(df)}")
print(f"Total enumerated population: {df['population_2023'].sum():,}")

# Top 5 most populous districts
top5 = df.sort_values(by="population_2023", ascending=False)[["district", "province", "population_2023", "literacy_rate_pct"]].head(5)
print("\nTop 5 Most Populous Districts:")
print(top5.to_string(index=False))

# Provincial summary
prov_summary = df.groupby("province").agg({
    "population_2023": "sum",
    "district": "count",
    "area_sq_km": "sum"
}).rename(columns={"district": "district_count"})
print("\nProvincial Aggregation:")
print(prov_summary)
```

## Citation

```text
Pakistan Bureau of Statistics (PBS), "7th Population and Housing Census 2023", Government of Pakistan, curated and structured by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
