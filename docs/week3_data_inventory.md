# Week 3 – Data Inventory

## Project context
**Project:** AI-Powered Contract and Terms & Conditions Analyzer  
**Selected pathway:** PDF and TXT document ingestion (Pathway A).  
**Data source:** CUAD v1 (Contract Understanding Atticus Dataset), real commercial contracts. No synthetic practice data is used.

## A1 – Requirement-to-data mapping

| Requirement ID | Needed information / feature | Candidate source | Why usable / constraint |
|---|---|---|---|
| **FR-03 / FR-05** (text extraction; cleaning and segmentation with context preserved) | Readable text from real contract PDF/TXT, split into clause-sized segments that keep their headings | CUAD v1 full-contract PDFs and TXTs | Real contract wording and layout. Limitation: commercial agreements, not consumer T&Cs. Some CUAD PDFs are scanned images and would need OCR (outside V1). |
| **NFR-04 / FR-06, FR-07** (accuracy measured on a labelled test set; clause identification and categorisation) | Expert clause labels for later evaluation | CUAD `master_clauses.csv` and `CUAD_v1.json` (41 clause categories) | Labels are not used in Topic 3. They are the reason CUAD suits later evaluation. |
| **NFR-06 / RAI-04** (public or authorised test documents) and **RAI-01 / NFR-05** (source grounding and traceability) | Licence, source identity, checksum, chunk-to-source link | CUAD (CC BY 4.0) plus `data/week3_manifest.json` | Redistributable with attribution. Contracts come from public filings; no private documents are used. |

**Attribution (CC BY 4.0):** Hendrycks, D., Burns, C., Chen, A., Ball, S. (2021). *CUAD: An Expert-Annotated NLP Dataset for Legal Contract Review.* arXiv:2103.06268. Obtained from https://huggingface.co/datasets/theatticusproject/cuad (510 contracts as PDF and TXT, plus expert clause labels).

## A4 – Data inventory

The notebook (cell 2) picks the files deterministically and prints their names. Fill in the two filenames and the SHA-256 values from the notebook output (cell A3).

| Source ID | Filename / URL | Type and purpose | Version / date / owner | Access / rights | Inspection evidence |
|---|---|---|---|---|---|
| S01 | `data/raw/CUAD_v1/full_contract_pdf/<fill in from notebook>.pdf` | Text-based contract PDF; demonstrates PDF extraction, cleaning and clause-aware chunking | CUAD v1; The Atticus Project | CC BY 4.0, attribution required | `<pages>` pages; `<chars>` extracted characters; SHA-256 `<fill in>` |
| S02 | `data/raw/CUAD_v1/full_contract_txt/<fill in from notebook>.txt` | Contract plain text; demonstrates TXT ingestion and clause-aware chunking | CUAD v1; The Atticus Project | CC BY 4.0, attribution required | `<chars>` characters; SHA-256 `<fill in>` |

**Raw vs prepared storage:** originals stay unchanged in `data/raw/`. Prepared output goes to `data/processed/prepared_text.jsonl`, with lineage in `data/week3_manifest.json`.

## Inspection observations
Fill in after running the notebook. Suggested points:
- Did PDF extraction return selectable text, or was the first PDF scanned (the notebook skips scanned PDFs automatically and reports how many it tried)?
- What clause headings do the contracts use (ARTICLE / Section / numbered)?
- Any extraction artefacts (page headers, footers, broken line wraps)?

## Project relevance and limitation
These files exercise the planned upload and extraction stages (FR-01 to FR-05) on real contract text. Two contracts are a very small sample and cannot support claims about clause-detection accuracy. CUAD is commercial contracts, so consumer-style T&C documents should be added later (RAI-05, varied document structures).

## Scope decision
Only PDF/TXT is implemented because it matches the document-upload workflow in the Topic 2 architecture. Tabular, image, JSON/API, audio and time-series pathways are outside the current project scope.

## Checkpoint A
The requirement that needs this data is **FR-03 / FR-05**, with **NFR-06 / RAI-01** for licence and provenance. The loaded sample is shown in notebook cell A3 (extracted text, character counts and SHA-256 for both files), not just a "file loaded" message.
