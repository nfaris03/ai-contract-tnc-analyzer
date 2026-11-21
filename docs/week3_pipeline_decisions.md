# Week 3 – Pipeline Decisions

## Selected pathway and dataset
- Pathway: PDF/TXT document ingestion (Pathway A).
- Dataset: CUAD v1 (real commercial contracts).
- Source: https://huggingface.co/datasets/theatticusproject/cuad
- Reason: The Topic 2 workflow begins with users uploading PDF documents. CUAD provides real contract documents and expert clause annotations that may support later clause-related development and evaluation.
- Limitation: CUAD represents commercial contracts and may not cover consumer website T&C wording.

## Executed sample
A matched PDF/TXT pair for the same Co-Branding and Advertising Agreement was extracted from the user-provided CUAD archive. The PDF had 9 pages and 29,376 extracted characters; the TXT contained 29,454 characters. Both sources passed non-empty text checks and SHA-256 fingerprints were recorded. These are two representations of one agreement, not two independent contracts.

## Pipeline stages
1. Initialise standard workspace folders (data/raw and data/processed).
2. Inspect the CUAD archive and extract the selected PDF/TXT pair.
3. Verify files recursively and record names and sizes.
4. Extract PDF text and read TXT using strict UTF-8 decoding.
5. Clean line endings, form feeds, repeated horizontal whitespace and excessive blank lines.
6. Compare fixed-size 1,000-character chunks with structure-aware chunks.
7. Export structure-aware chunks to JSONL with source filename and checksum.
8. Validate non-empty chunks and verify the saved JSONL reloads identically.
9. Run preparation a second time and compare outputs for repeatability.
10. Generate and verify source-to-output lineage metadata and SHA-256 checksums.

## Preparation comparison

| Source | Fixed-size chunks | Structure-aware chunks | Lowercase-start proxy | Structure chunks starting at detected heading |
|---|---:|---:|---:|---:|
| PDF | 29 | 18 | 22 | 12 |
| TXT | 29 | 15 | 22 | 7 |

**Selected approach:** Structure-aware chunking. It attempts to keep headings with the associated clause text, supporting context preservation and later source traceability. Fixed-size chunking remains a baseline. The lowercase-start measure is only a rough proxy for a possible mid-sentence cut, not a definitive linguistic evaluation.

## Extraction and cleaning decisions
- PDF extraction: pypdf, targeting text-based PDFs.
- TXT extraction: UTF-8 decoding with strict error handling.
- Cleaning: normalise line endings and form feeds, collapse repeated horizontal whitespace, reduce excessive blank lines, and trim outer whitespace.
- Preserve headings and clause numbering where detected.
- Chunking: heading/paragraph-based segmentation; merge fragments shorter than 80 characters; split chunks longer than 3,000 characters at blank lines, with fixed cuts as a fallback for a long paragraph.

## Validation and lineage results
- Input files found and inspected: PASS.
- PDF text extraction: PASS (9 pages; 29,376 characters).
- TXT UTF-8 decoding: PASS (29,454 characters).
- Prepared output exists and is non-empty: PASS (69,860 bytes; 33 records).
- JSONL reload matches in-memory records: PASS.
- All chunks non-empty: PASS.
- Repeatability: PASS; second run produced identical structure-aware chunks.
- Source/output SHA-256 lineage recorded and verified: PASS.

## Potential failure points and responses
1. Scanned or image-only PDF: extraction may return little or no text. OCR is outside this version; stop and flag the source rather than treating empty text as valid.
2. Missing source or unsupported file: stop with a clear path/format error.
3. TXT encoding issue: strict UTF-8 decoding surfaces the problem rather than silently dropping characters.
4. Unrecognised clause headings: paragraph-block fallback is used; resulting chunks still require manual inspection.
5. Redistribution restrictions: raw documents and extracted text are kept out of the public repository until document-level rights are checked.

## Limitations
- The PDF and TXT are two formats of one agreement, not two independent contracts.
- Only one agreement pair was processed in this run; this is a pipeline demonstration, not representative dataset evaluation.
- CUAD contains commercial contracts and may not represent consumer website T&Cs.
- Heading detection is rule-based and may split unusual formats imperfectly.
- OCR, password-protected PDFs, complex layouts, multilingual extraction, model training and clause-detection accuracy evaluation are outside this pipeline version.
- The notebook was executed locally; the included Colab upload workflow has not been tested in the student's own Colab account.


---

## UNCOVER AI — Additive Project Extension (Planned)

**Updated proposed title:** UNCOVER AI: An AI-Powered Contract Analysis and Document Review Management System.

The existing AI contract/T&C analyzer remains the **core FYP component**: upload text-based PDFs, extract and prepare text, identify and categorize clauses, provide plain-language explanations, and show the supporting original excerpts. The application is now intended for **both individuals and organizational users**.

**Additional planned supporting features:**
- **Dashboard:** counts of total documents, pending review, reviewed, user-approved, and needs-attention documents; recent uploads; and a chart of detected clause categories.
- **My Documents:** saved document and analysis history, search/filter, reopen, and deletion.
- **Review Management:** user-controlled review statuses and notes, tracked separately from AI findings or processing status.
- **PDF Reports:** export identified clauses, supporting source excerpts, explanations, and limitations.
- **Basic accounts and storage:** user-specific access and document metadata/analysis persistence (SQLite proposed for the prototype).

**Important:** These are proposed additions, **not implemented or evaluated features**. An 'approved' status is a user's workflow decision, not an AI legal-safety judgment. AI-generated attention indicators must not be presented as legal conclusions. Existing lecturer lab activities and reported results remain unchanged. See [UNCOVER AI scope extension](uncover_ai_scope_extension.md) for details.

**Pipeline integration extension:** Preserve the existing PDF/TXT extraction, cleaning, chunking, JSONL lineage, and repeatability tests. Once clause analysis is implemented, persist results with source references; dashboard and review features consume these results. The current one-agreement pipeline demonstration does not establish model accuracy or dashboard functionality.


## Week 3 submission gap and reproducibility notes
- The submitted notebook currently contains code but no saved execution outputs. The manifest documents a prior local execution; a fresh run by the student, including Cell 9, is still needed for directly inspectable execution evidence.
- `data/processed/prepared_text.jsonl` is intentionally not public because it contains extracted contract text. To meet the output-deliverable requirement without sharing unreviewed material, produce an explicitly **synthetic** small JSONL demonstration or obtain lecturer approval for a private/authorized output submission. Do not label synthetic examples as CUAD-derived.
- The V1 run manifest is under `data/pipeline_v1/pdf/`; executed content output is not currently in the public repository. Preserve the original local-run hashes as historical evidence; new runs should create new manifests rather than overwrite them with invented success values.
- The diagram source is `docs/week3_pipeline_diagram.svg`; the requested `.png` should be exported and committed.

### Reflection to complete personally
Record where you executed the notebook, what actually failed on the first attempt, how you fixed it, and the actual Cell 9 output. These details cannot be inferred from documentation alone.
