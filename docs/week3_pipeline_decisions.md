# Week 3 – Pipeline Decisions

## Selected pathway and dataset
- Pathway: PDF/TXT document ingestion.
- Dataset: CUAD v1 (real commercial contracts).
- Source: https://huggingface.co/datasets/theatticusproject/cuad
- Reason: The Topic 2 workflow begins with uploaded PDF documents. CUAD provides real contract text and expert clause annotations that may support later evaluation.
- Limitation: CUAD represents commercial contracts and may not cover consumer website T&C wording.

## Planned pipeline
1. Create raw and processed folders in the Colab workspace.
2. Download a text-extractable PDF and a TXT contract from CUAD.
3. Inspect filenames, file sizes, extracted text, page count where applicable, and SHA-256.
4. Extract PDF text and read TXT using strict UTF-8 decoding.
5. Clean line endings and repeated whitespace while retaining meaningful headings and paragraph boundaries.
6. Compare fixed-size 1,000-character chunks with structure-aware chunks.
7. Export structure-aware chunks to JSONL with source filename and checksum.
8. Validate non-empty chunks and verify the saved JSONL can be reopened identically.
9. Run preparation a second time and compare outputs for repeatability.
10. Generate and verify a source-to-output lineage manifest.

## Preparation comparison
The notebook contains a comparison of fixed-size and structure-aware chunking. Counts and observations must be filled only after execution.

| Source | Fixed-size chunk count | Structure-aware chunk count | Fixed chunks beginning mid-sentence |
|---|---:|---:|---:|
| S01 PDF | Pending | Pending | Pending |
| S02 TXT | Pending | Pending | Pending |

**Proposed selection:** Structure-aware chunking, if inspection confirms that detected headings preserve meaningful clause boundaries. It is preferred because keeping a clause heading with its text can preserve context and improve traceability. Fixed-size chunking is retained as a baseline because it is simple and reproducible but may split clauses mid-sentence.

## Extraction and cleaning decisions
- PDF extraction: pypdf, targeting text-based PDFs.
- TXT extraction: UTF-8 decoding with strict error handling.
- Cleaning: normalise line endings and form feeds, collapse repeated horizontal whitespace, reduce excessive blank lines, and trim outer whitespace.
- Preserve headings and clause numbering because they provide context.

## Validation and lineage
The notebook is designed to check source files, non-empty extracted text and chunks, successful JSONL reload, repeatability, and source/prepared-output checksums in a lineage manifest.

These are planned checks. They must not be reported as passed until the notebook has been run successfully and the output inspected.

## Potential failure points and responses
1. Scanned or image-only PDF: text extraction may return little or no text. The notebook tries a limited number of candidate PDFs and selects one with at least 1,000 extracted characters. OCR is outside this version.
2. Missing source or unsupported file: stop with a clear file/path error rather than creating an empty output.
3. TXT encoding issue: strict UTF-8 decoding surfaces the problem instead of silently dropping characters.
4. Unrecognised clause headings: use paragraph-block fallback; inspect resulting chunks because fallback segmentation may not preserve clause boundaries reliably.

## Limitations and current status
- The notebook has been authored but its execution has not yet been verified.
- The selected sample is two contracts, not the full CUAD dataset.
- No model is trained and no clause-detection accuracy is measured by this pipeline.
- CUAD is commercial-contract data; consumer T&C coverage remains a gap.
- OCR, password-protected PDFs, complex layouts, and multilingual extraction are outside this version.
