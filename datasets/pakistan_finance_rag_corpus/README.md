# Pakistan Finance RAG Corpus

## Summary

This dataset is a retrieval-augmented generation corpus for Pakistan finance, inflation, and government securities. It is separate from the numeric ML feature package. It contains source-document metadata, retrieval chunks, and citation-backed QA/evaluation pairs.

## Dataset Details

- **Dataset ID**: `pakistan-finance-rag-corpus`
- **Version**: `0.1.0`
- **Category**: `Economy and Finance`
- **Tags**: `rag`, `finance`, `inflation`, `cpi`, `spi`, `wpi`, `bonds`, `yields`, `pakistan`, `pbs`, `sbp`
- **Language**: `English`
- **Geography**: `Pakistan`
- **File Formats**: `CSV`
- **Records**: `43 documents`, `5,249 chunks`, `148 QA pairs`
- **Maintainer**: `OpenDoc Data Stewardship Team`

## Source and Provenance

- **PBS Price Statistics**: https://www.pbs.gov.pk/price-statistics/
- **PBS historical indices PDF**: https://www.pbs.gov.pk/wp-content/uploads/2020/07/indices.pdf
- **PBS June 2026 monthly review**: https://www.pbs.gov.pk/wp-content/uploads/2020/07/Monthly-Review-June-2026.pdf
- **SBP T-bill workbook**: https://www.sbp.org.pk/assets/document/tb.xlsx
- **SBP PIB workbook**: https://www.sbp.org.pk/assets/document/Pakinvestbonds.xlsx

The corpus was built from official source PDFs, official PBS weekly report workbooks, and table resources already curated in the finance datasets. Staff-name pages from the monthly review were excluded because they are not useful retrieval content.

## License

- **Original License**: PBS/SBP public website data; explicit open redistribution licenses not found.
- **Repository License**: `LicenseRef-PBS-Public-Website` and `LicenseRef-SBP-Public-Website`
- **Attribution Required**: Yes, cite PBS and/or SBP.
- **Restriction**: Do not label as CC-BY or public domain unless the agencies publish explicit open-license terms.

## Files

- `rag_documents.csv`: source document/table metadata.
- `rag_chunks.csv`: retrieval chunks with source URL, locator, text, token estimate, and topic tags.
- `rag_qa_pairs.csv`: fact-lookup QA pairs with evidence chunk IDs and train/validation/test split.

## Quality Report

- **Duplicate IDs**: 0
- **Blank IDs**: 0
- **QA Evidence Coverage**: 100% of QA pairs have valid evidence chunk IDs.
- **PII Scan**: 0 email/phone regex hits after filtering non-retrieval staff pages and rounding long decimal text.
- **Known Limitation**: QA pairs are deterministic fact-lookup questions, not adversarial reasoning tests.

## Intended Use

Appropriate for:
- Finance/inflation RAG retrieval experiments.
- Citation-grounded QA evaluation.
- Domain glossary and assistant grounding.

Out of scope:
- Numeric forecasting model training; use `pakistan_finance_ml_features` instead.
- Legal, trading, or investment advice.

## Citation

```text
Pakistan Bureau of Statistics and State Bank of Pakistan public finance publications, curated as "Pakistan Finance RAG Corpus" by OpenDoc Pakistan (OpenDoc), v0.1.0, 2026.
```
