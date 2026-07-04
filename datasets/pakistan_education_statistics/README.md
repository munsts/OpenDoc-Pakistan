# Pakistan Education Statistics 2024

## Summary

This dataset compiles key educational indicators across major districts of Pakistan for the year 2024, including literacy rates, primary/secondary school enrollment numbers, and the total count of educational institutions. It serves as a foundational dataset for analyzing educational equity, literacy distribution, and regional developmental gaps.

## Dataset Details

- **Dataset ID**: `pakistan-education-statistics`
- **Version**: `1.0.0`
- **Category**: `Education`
- **Tags**: `education`, `literacy`, `schools`, `enrollment`, `districts`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan (all provinces, ICT, AJK, Gilgit-Baltistan)`
- **Time Period**: `2024`
- **File Formats**: `CSV`
- **Size**: `1 KB`
- **Update Frequency**: `Annually`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: Pakistan Bureau of Statistics (PBS) & Provincial Education Departments
- **Source URL**: https://www.pbs.gov.pk
- **Source Type**: Official Government Portals & Annual Reports
- **Collection Method**: Aggregated from provincial educational census reports and public statistical databases.
- **Collection Date**: January 2026
- **Processing Pipeline**: Standardized district names, computed rates, and formatted headers into standard tidy CSV format.
- **Raw Data Availability**: Publicly available on source websites.

## License

- **Original License**: Open Government Data License (OGDL) Pakistan
- **Repository License**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Redistribution**: Allowed
- **Restrictions**: Must credit Pakistan Bureau of Statistics and OpenDoc Pakistan.

## Intended Use

Appropriate for:
- Spatial mapping of literacy rates across Pakistan.
- Correlation analysis between the number of schools and school enrollment levels.
- Policy research and educational infrastructure planning.

## Out-of-Scope Use

Prohibited or discouraged uses:
- Drawing conclusions on individual school quality (as data is aggregated at the district level).
- Real-time tracker (this represents a static annual statistical compilation).

## Data Structure

The dataset contains a single CSV file under `data/processed/education_statistics.csv`.
Columns:
- `district` (string): Name of the administrative district.
- `province` (string): Province or administrative territory.
- `literacy_rate_pct` (number): Literacy rate percentage of the district population.
- `primary_enrollment` (integer): Total student enrollment in primary schools (grades 1-5).
- `secondary_enrollment` (integer): Total student enrollment in secondary schools (grades 6-10).
- `number_of_schools` (integer): Total number of functioning public/registered private schools.
- `year` (integer): Calendar year representing the data.

## Data Dictionary

Detailed field definitions are available in [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 98 / 100
- **Rating**: Excellent
- **Missing Values**: 0%
- **Duplicate Rows**: 0%
- **Validation Status**: Passed
- **Known Issues**: None.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (No personal data present; fully aggregated district stats)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None required.
- **Reviewer**: OpenDoc Compliance Board
- **Review Date**: July 3, 2026

## Bias, Gaps, and Limitations

- Under-registration of informal private schools in rural areas may lead to slight undercounts in the total number of schools and enrollment metrics.
- Literacy definition follows the standard PBS census definition (ability to read and write a basic paragraph in any language with understanding).

## Example Usage

```python
import pandas as pd

# Load dataset
df = pd.read_csv("data/processed/education_statistics.csv")
print(df.head())

# Find top 5 districts by literacy rate
top_districts = df.sort_values(by="literacy_rate_pct", ascending=False).head(5)
print(top_districts)
```

## Citation

Please cite this dataset as:
```text
Pakistan Bureau of Statistics, "Pakistan Education Statistics 2024", curated by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
