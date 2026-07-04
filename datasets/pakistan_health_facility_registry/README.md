# Pakistan Health Facility Registry (Geolocated)

## Summary

A geolocated registry of health facilities across Pakistan — hospitals, clinics, dispensaries, doctors, dentists, and pharmacies — with facility type, operator, bed counts (where tagged), and WGS84 coordinates. It is derived from the OpenStreetMap-based healthsites.io export published on Open Data Pakistan. Personal-identifier columns present in the raw export (contact phone numbers, editor usernames, per-staff fields, UUIDs) have been **removed** during processing. Useful for health-access mapping, facility-density analysis, and geospatial ML.

## Dataset Details

- **Dataset ID**: `pakistan-health-facility-registry`
- **Version**: `1.0.0`
- **Category**: `Health`
- **Tags**: `health-facilities`, `hospitals`, `clinics`, `geospatial`, `healthsites`, `osm`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan (nationwide, point locations)`
- **File Formats**: `CSV`
- **Records**: `2,997 facilities (2,872 named)`
- **Update Frequency**: `Irregular (as source/OSM is refreshed)`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: Open Data Pakistan — "Pakistan Health Sites" (healthsites.io / OpenStreetMap export)
- **Source URL**: https://opendata.com.pk/dataset/pakistan-health-sites
- **Source Type**: Open-data portal CSV resource, originating from OpenStreetMap contributors via healthsites.io
- **Collection Method**: Direct download of the published CSV resource.
- **Collection Date**: July 2026
- **Processing Pipeline**: Selected facility-attribute columns; **dropped PII columns** (`contact_number`, `changeset_user`, `uuid`, `staff_doctors`, `staff_nurses`, changeset metadata); normalised `facility_type` (healthcare tag, falling back to amenity); kept rows with a name or a coordinate pair.
- **Raw Data Availability**: Public on the ODP portal and healthsites.io.

## License

- **Original License**: Open Database License (ODbL) 1.0 — inherited from OpenStreetMap.
- **Repository License**: ODbL 1.0 (share-alike; retained to comply with the source license).
- **Attribution Required**: Yes — "© OpenStreetMap contributors".
- **Commercial Use**: Allowed under ODbL terms.
- **Redistribution**: Allowed under ODbL (derivative databases must remain ODbL).
- **Restrictions**: Must attribute OpenStreetMap contributors and healthsites.io; share-alike applies.

## Intended Use

Appropriate for:
- Mapping health-facility access and geographic coverage gaps.
- Facility-density and catchment analysis.
- Geospatial ML (clustering, accessibility modelling).

## Out-of-Scope Use

- Authoritative facility licensing/accreditation decisions — this is crowd-sourced OSM data, not an official registry.
- Contacting facilities — contact details have been intentionally removed.

## Data Structure

Single CSV at `data/processed/health_facilities.csv`. One row per facility (point). See the data dictionary for all columns.

## Data Dictionary

See [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 85 / 100
- **Rating**: Good (deductions: sparsely populated optional OSM columns; ODbL not in the scorer's open-license whitelist despite being an open license)
- **Records**: 2,997 facilities; 2,872 have a name.
- **Missing Values**: Many optional OSM tags (beds, operator, speciality, address) are sparsely populated — this reflects OSM coverage.
- **Validation Status**: Passes Frictionless tabular-data-resource schema.
- **Known Issues**: Coordinates and completeness vary; some points may be duplicated or stale in the underlying OSM data.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 after redaction (facility locations are public infrastructure).
- **Personal Data Present**: No (contact numbers, editor usernames, and per-staff fields removed).
- **Sensitive Data Present**: No.
- **Redactions Applied**: Dropped `contact_number`, `changeset_user`, `uuid`, `staff_doctors`, `staff_nurses`, and changeset metadata columns.
- **Reviewer**: OpenDoc Compliance Board

## Bias, Gaps, and Limitations

- OSM coverage skews toward urban centres; rural facilities are under-represented.
- Facility typing depends on volunteer tagging quality and is not standardised to a national health taxonomy.

## Example Usage

```python
import pandas as pd

df = pd.read_csv("data/processed/health_facilities.csv")

# Count facilities by type
print(df["facility_type"].value_counts().head(10))

# Hospitals with recorded coordinates
hospitals = df[(df["facility_type"] == "hospital") & df["latitude"].notna()]
print(len(hospitals))
```

## Citation

```text
OpenStreetMap contributors / healthsites.io via Open Data Pakistan, "Pakistan Health Sites", curated as "Pakistan Health Facility Registry" by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026. © OpenStreetMap contributors, ODbL.
```
