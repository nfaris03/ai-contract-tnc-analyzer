# Week 3 – Data Inventory

## Project context
- Project: AI-Powered Contract and Terms & Conditions Analyzer
- Selected pathway: PDF/TXT document ingestion (Pathway A)
- Dataset: CUAD v1 (Contract Understanding Atticus Dataset)
- User-provided archive: CUAD_v1 (1).zip (105,883,672 bytes)
- Dataset source: https://huggingface.co/datasets/theatticusproject/cuad
- Dataset paper: Hendrycks et al. (2021), CUAD: An Expert-Annotated NLP Dataset for Legal Contract Review, arXiv:2103.06268.

CUAD contains commercial contracts and expert clause annotations. It is relevant to contract clause extraction and later evaluation, but it does not fully represent consumer website Terms & Conditions.

## A1 – Requirement-to-data mapping

| Requirement | Needed data | CUAD component | Use and limitation |
|---|---|---|---|
| FR-03 / FR-05 | Contract text for extraction, cleaning and segmentation | Full-contract PDF and TXT files | Supports document ingestion and context-preserving preparation. |
| FR-06 / FR-07 / NFR-04 | Clause examples and labels for identification and categorisation | CUAD_v1.json, master_clauses.csv, and category annotation files | Supports later labelled clause work; annotations were not used in this Week 3 PDF/TXT pipeline. |
| NFR-05 / RAI-01 / RAI-04 | Source identity, provenance, traceability and permitted access | Original files, source metadata and checksums | SHA-256 lineage is recorded. Verify dataset release terms and each underlying contract's redistribution conditions before sharing. |

## A2 – Source identity and access
- Dataset: CUAD v1; publisher: The Atticus Project.
- Research citation: Hendrycks et al. (2021), arXiv:2103.06268.
- Dataset page: https://huggingface.co/datasets/theatticusproject/cuad
- Archive size: 105,883,672 bytes.
- Archive SHA-256: 88b694d99007d39777fa44cd72daf8297773d285dc3eab0091ba32078888d18e.
- Redistribution note: the dataset release is described as CC BY 4.0, but this is not blanket permission to redistribute every underlying contract or extracted text. Raw contract files and prepared text are excluded from this public repository pending document-level review.

## A3 – Representative file inspection (executed)
The pipeline selected a matched PDF/TXT pair for the same Co-Branding and Advertising Agreement. This is two formats of one contract, not two independent contracts. The PDF contains selectable text and the TXT decodes as UTF-8.

| Source | Format | Size (bytes) | Pages / segments | Extracted characters | SHA-256 |
|---|---:|---:|---:|---:|---|
| Co-Branding and Advertising Agreement | PDF | 109,658 | 9 pages | 29,376 | db445255a65067160b9e9a7cf23afbd3379a715d000b0576fa8e7f64982e523c |
| Co-Branding and Advertising Agreement | TXT | 29,454 | 1 text file | 29,454 | 6cdfab95eb5b30c0d2d4860c8204b96b36a54cb9e2025c5ceb1457d223afac41 |

Both sources produced non-empty text exceeding 1,000 characters. PDF extraction and strict UTF-8 TXT reading completed successfully. The two formats produced similar but not identical character counts because PDF extraction preserves layout artefacts differently from the supplied TXT.

## A4 – Inspection observations
- PDF: 9 pages; selectable text extracted successfully (29,376 characters).
- TXT: UTF-8 decoding succeeded (29,454 characters).
- Both formats represent the same agreement, allowing a comparison of extraction output across formats.
- PDF extraction may introduce spacing, line-wrap and layout differences compared with the text source.
- No OCR was required for this selected PDF. Scanned PDFs and complex-layout edge cases were not tested.

## B2/B3 – Preparation and comparison evidence
The pipeline cleaned line endings, form feeds, repeated horizontal whitespace and excessive blank lines. It compared fixed-size 1,000-character chunks with structure-aware chunks that use detected headings/paragraph boundaries, merge fragments shorter than 80 characters, and cap chunks at 3,000 characters.

| Source | Fixed-size chunks | Structure-aware chunks | Fixed chunks starting lowercase (rough proxy) | Structure chunks starting with detected heading |
|---|---:|---:|---:|---:|
| PDF | 29 | 18 | 22 | 12 |
| TXT | 29 | 15 | 22 | 7 |

The selected approach is structure-aware chunking because it attempts to keep clause/section headings with their text. The lowercase-start count is only a rough diagnostic, not a definitive sentence-boundary metric. Heading detection is rule-based and may miss unusual heading styles.

## B4 – Outputs and validation
- Prepared output: data/processed/prepared_text.jsonl (generated locally; contains extracted contract text and is not committed to the public repository).
- Prepared records: 33 chunks (18 from PDF + 15 from TXT).
- Prepared output size: 69,860 bytes.
- Prepared output SHA-256: 628db70cdb428d6e3ca3d1858999c818e812a84cca0bbe8628e880408146aca0.
- JSONL read-back matched the in-memory records; all chunks were non-empty.
- A second preparation run produced identical structure-aware chunks.
- Source and output checksums were recorded in data/week3_manifest.json.
- Pipeline run metadata is recorded in data/pipeline_v1/pdf/pipeline_manifest.json.

## Storage and lineage plan
- data/raw/: local, unchanged source files during processing; excluded from GitHub.
- data/processed/prepared_text.jsonl: local prepared chunks; contains contract text and excluded from public GitHub pending rights review.
- data/week3_manifest.json: source filenames, sizes, SHA-256 values, output checksum, processing description, comparison evidence and validation status.
- data/pipeline_v1/pdf/pipeline_manifest.json: concise V1 pipeline execution summary and limitations.

## Project relevance and limitations
CUAD supports contract-text ingestion and clause preparation and provides annotations that may support later clause identification/evaluation. This Week 3 run demonstrates data ingestion and preparation only; no model was trained and no clause-detection accuracy was measured. CUAD is commercial-contract data and consumer T&C coverage remains a gap.

## Scope decision
Only PDF/TXT ingestion is selected because it aligns with the Topic 2 document-upload workflow. Tabular, image, JSON/API, audio and time-series pathways are outside the current project scope.

**Execution note:** The notebook was executed successfully in a local Python/Jupyter kernel against the supplied archive. The notebook includes a Google Colab upload workflow, but that workflow has not been run in the student's own Colab account. The local execution evidence is recorded in the manifest.
