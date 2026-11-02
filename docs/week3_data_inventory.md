# Week 3 – Data Inventory

## Project context
**Project:** AI-Powered Contract and Terms & Conditions Analyzer  
**Selected pathway:** PDF and TXT document ingestion (Pathway A).  
**Data source type:** Synthetic practice dataset (`Topic_3_Dummy_Datasets.zip`, `01_documents`), used because no permission-checked contract dataset has been selected yet.

## A1 – Requirement-to-data mapping

| Requirement ID | Needed information / feature | Candidate source | Why usable / constraint |
|---|---|---|---|
| **FR-03 / FR-05** (text extraction; cleaning and segmentation with context preserved) | Readable text from an uploaded PDF/TXT, split into sections that keep their headings | **Now:** synthetic `student_handbook_demo.pdf` and `faq_demo.txt`. **Later:** public T&C documents or authorised sample agreements | The synthetic files exercise extraction and chunking only. They contain no contract clauses, so they cannot support FR-06/FR-07 or NFR-04 claims. |
| **NFR-06 / RAI-04** (test documents public or authorised) and **RAI-01 / NFR-05** (source grounding and traceability) | Source identity, owner, access rights, checksum, and a link from each chunk back to its source | Same files plus `data/week3_manifest.json` | Synthetic, redistributable teaching data is safe to keep in GitHub. Real contracts must be public or authorised before they enter the repo. |

**Replacement plan:** the synthetic pack will be replaced by a permission-checked contract / T&C dataset (public T&C documents or authorised sample agreements), selected separately for clause detection and evaluation. Results on the practice files must not be read as evidence of the application's performance.

## A4 – Data inventory

| Source ID | Filename / URL | Type and purpose | Version / date / owner | Access / rights | Inspection evidence |
|---|---|---|---|---|---|
| S01 | `data/raw/student_handbook_demo.pdf` | Text-based PDF; demonstrates PDF extraction, cleaning and section-aware chunking | "2026 Demo Edition"; owner "Teaching Team" (stated in the document) | Lecturer-supplied synthetic teaching data; lab use only | 1 page; 426 extracted characters (425 after cleaning); title/metadata line plus four sections (Registration, Attendance, Graduation, Academic Support); no contract clauses. SHA-256 `3dc6270e4a2d072afe07502c27c0bb71a2305bf2e020f01cc86fe96d7950ec5e` |
| S02 | `data/raw/faq_demo.txt` | UTF-8 plain text; demonstrates TXT ingestion and keeping Q&A pairs together | Version, date and owner not stated | Lecturer-supplied synthetic teaching data; lab use only | 171 bytes; 170 characters after cleaning; title line plus two Q&A pairs. SHA-256 `05461ed704d8c8cf8b7a609e2b4b4e7cb800a7fe16a68fe5805546a7b3e2f43f` |

**Raw vs prepared storage:** originals stay unchanged in `data/raw/`. Prepared output goes to `data/processed/` (`prepared_text.jsonl`), with lineage in `data/week3_manifest.json`.

## Inspection observations
- PDF text extraction returned selectable text, so OCR was not needed for this sample.
- PDF section headings provide useful chunk boundaries.
- Blank lines separate the TXT FAQ pairs, so each Q&A pair can stay together.
- Both samples are small and synthetic.

## Project relevance and limitation
These files exercise basic document-ingestion mechanics relevant to the planned upload feature (FR-01 to FR-05). They are not project-domain contract data and cannot support claims about clause detection, legal-risk classification or model accuracy.

## Scope decision
Only PDF/TXT is implemented because it matches the document-upload workflow in the Topic 2 architecture. Tabular, image, JSON/API, audio and time-series pathways in the ZIP are outside the current project scope.

## Checkpoint A
The requirement that needs this data is **FR-03 / FR-05**, with **NFR-06 / RAI-01** for provenance. The loaded sample is shown in notebook cell A3 (extracted text, character counts and SHA-256 for both files), not just a "file loaded" message.
