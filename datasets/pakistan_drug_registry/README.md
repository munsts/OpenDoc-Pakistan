# Pakistan Pharmaceutical Product Registry (RAG Corpus)

## Summary

A retrieval-augmented-generation (RAG) ready corpus of medicines relevant to Pakistan, in **two parts**:

1. **Marketed products** — pharmaceutical products sold in Pakistan with retail prices (before/after discount), pack sizes, manufacturers, and market availability (321 products).
2. **Essential medicines** — Pakistan's National Essential Medicines List (WHO Model List, 23rd List 2023), with therapeutic category, listing type (core/complementary), and dosage forms/strengths (398 medicines).

Each part ships in two equivalent formats: a **JSONL** corpus (one embeddable passage plus structured metadata per record) for RAG / vector-search pipelines, and a **flat CSV** for tabular ML and quick validation. This is the reference dataset defining OpenDoc's RAG corpus convention.

## Dataset Details

- **Dataset ID**: `pakistan-drug-registry`
- **Version**: `1.0.0`
- **Category**: `Health`
- **Tags**: `drugs`, `medicines`, `pharmaceutical`, `prices`, `rag`, `healthcare`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan`
- **File Formats**: `JSONL`, `CSV`
- **Records**: `321 marketed products (83 companies) + 398 essential medicines (19 therapeutic categories)`
- **Version**: `1.1.0`
- **Update Frequency**: `Irregular (as sources are refreshed)`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **Source Name**: Open Data Pakistan (ODP) — "Pharmaceutical product pricing and availability in Pakistan" (originally published on Kaggle by Talha Sattar)
- **Source URL**: https://opendata.com.pk/dataset/pharmaceutical-product-pricing-and-availability-in-pakistan
- **Upstream Source**: https://www.kaggle.com/datasets/talhasattar727/pakistan-pharmaceutical-dataset
- **Source Type**: Open-data portal CSV resource (CKAN), sourced from a Kaggle dataset (secondary research)
- **Collection Method**: Direct download of the published CSV resource.
- **Collection Date**: July 2026
- **Processing Pipeline**: Deduplicated rows, parsed prices into integer PKR amounts, parsed discount percentages, generated a stable id per product, and synthesised a natural-language `text` passage per record for embedding. Emitted both JSONL and CSV.
- **Raw Data Availability**: Public on the ODP portal.

## License

- **Marketed products** — Original License: MIT (as declared on the upstream Kaggle source). Redistributed under MIT.
- **Essential medicines** — Source: Government of Pakistan gazette notification S.R.O. 1423(I)/2023 (public statutory notification) adopting the WHO Model List of Essential Medicines. WHO Model List content is © WHO, reproduced here for reference from the public gazette; WHO material is generally reusable with attribution under WHO's terms.
- **Attribution Required**: Yes
- **Commercial Use**: Allowed (marketed-products part under MIT)
- **Redistribution**: Allowed
- **Restrictions**: Retain the MIT notice and credit Talha Sattar & Open Data Pakistan (products); credit MoNHSR&C / WHO (essential medicines); and credit OpenDoc Pakistan.

## Intended Use

Appropriate for:
- Building RAG chatbots / assistants that answer questions about Pakistani medicine prices and availability.
- Vector-search and semantic-retrieval demos over a domain corpus.
- Tabular price analysis and ML (via the CSV twin).

## Out-of-Scope Use

- **Not medical advice.** Contains no dosing, indication, contraindication, or safety information.
- Not a complete or official drug registry — it is a market price/availability snapshot, not the DRAP master registration list.
- Prices are point-in-time and will drift; do not use for current billing.

## Data Structure

Marketed products (source: Open Data Pakistan / Kaggle, MIT):
- `data/processed/drug_registry.jsonl` — one JSON object per line: `{id, text, metadata{product_name, company, pack_size, price_before_pkr, discount_percent, price_after_pkr, availability, country, source}}`.
- `data/processed/drug_registry.csv` — flat equivalent with the metadata fields plus the `text` column.

Essential medicines (source: Pakistan gazette S.R.O. 1423(I)/2023 adopting the WHO Model List of Essential Medicines, 23rd List 2023):
- `data/processed/essential_medicines.jsonl` — `{id, text, metadata{medicine, therapeutic_category, subcategory, list_type, dosage_forms, country, source}}`.
- `data/processed/essential_medicines.csv` — flat equivalent.

The essential-medicines part was extracted from the WHO-hosted PDF of the Pakistan NEML gazette using automated PDF parsing (firecrawl `parse`), then structured by therapeutic section.

## Data Dictionary

See [data_dictionary.csv](data_dictionary.csv).

## Quality Report

- **Quality Score**: 99 / 100
- **Rating**: Excellent
- **Records**: 321 unique products (exact and price/pack duplicates removed).
- **Duplicate Rows**: 0% (primary key: `id`).
- **Validation Status**: CSV twin passes Frictionless tabular-data-resource schema.
- **Known Issues**: Some products share a brand name with different pack sizes/prices (kept as distinct records). Company names are as-listed and not normalised to legal entity names.

## Privacy and Sensitivity Review

- **Privacy Level**: P0 (commercial product listings; no personal data)
- **Personal Data Present**: No
- **Sensitive Data Present**: No
- **Redactions Applied**: None

## Bias, Gaps, and Limitations

- Marketed-products coverage is limited to the source snapshot; not exhaustive of the Pakistani market.
- The marketed-products and essential-medicines parts are not cross-linked (brand↔generic mapping is out of scope for this version).
- Essential-medicines entries were extracted via automated PDF parsing; dosage-form strings are as-listed and may contain minor OCR/formatting artefacts.

## Example Usage

```python
import json

# Load the RAG corpus
with open("data/processed/drug_registry.jsonl", encoding="utf-8") as f:
    docs = [json.loads(line) for line in f]

# Each doc is ready to embed
print(docs[0]["text"])
print(docs[0]["metadata"]["price_after_pkr"])
```

## Citation

```text
Open Data Pakistan, "Pharmaceutical product pricing and availability in Pakistan", curated as "Pakistan Pharmaceutical Product Registry (RAG Corpus)" by OpenDoc Pakistan (OpenDoc), v1.0.0, 2026.
```
