# Pakistan Pharmaceutical Product Registry (RAG Corpus)

## Summary

A retrieval-augmented-generation (RAG) ready corpus of pharmaceutical products marketed in Pakistan, including retail prices (before/after discount), pack sizes, manufacturers, and market availability. It ships in two equivalent formats: a **JSONL** corpus (one embeddable passage plus structured metadata per product) for RAG / vector-search pipelines, and a **flat CSV** for tabular ML and quick validation. This is the reference dataset defining OpenDoc's RAG corpus convention.

## Dataset Details

- **Dataset ID**: `pakistan-drug-registry`
- **Version**: `1.0.0`
- **Category**: `Health`
- **Tags**: `drugs`, `medicines`, `pharmaceutical`, `prices`, `rag`, `healthcare`, `pakistan`
- **Language**: `English`
- **Geography**: `Pakistan`
- **File Formats**: `JSONL`, `CSV`
- **Records**: `321 unique products across 83 companies`
- **Update Frequency**: `Irregular (as source is refreshed)`
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

- **Original License**: MIT License (as declared on the upstream Kaggle source).
- **Repository License**: MIT License (retained from source).
- **Attribution Required**: Yes
- **Commercial Use**: Allowed
- **Redistribution**: Allowed
- **Restrictions**: Must retain the MIT notice and credit Talha Sattar, Open Data Pakistan, and OpenDoc Pakistan.

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

- `data/processed/drug_registry.jsonl` — one JSON object per line: `{id, text, metadata{product_name, company, pack_size, price_before_pkr, discount_percent, price_after_pkr, availability, country, source}}`.
- `data/processed/drug_registry.csv` — flat equivalent with the metadata fields plus the `text` column.

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

- Coverage is limited to products present in the source snapshot; not exhaustive of the Pakistani market.
- No therapeutic/composition metadata — enrichment from the DRAP essential-medicines gazette (PDF, via OCR) is a planned future version.

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
