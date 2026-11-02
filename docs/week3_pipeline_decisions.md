# Week 3 – Pipeline Decisions

## Selected pathway
PDF and TXT document ingestion, aligned with the document-upload workflow in the Topic 2 architecture (FR-01 to FR-05). Data: CUAD v1 real contracts (CC BY 4.0).

## Preparation comparison

Two approaches were run on the same two contracts (one PDF, one TXT). Record the observed counts from the notebook (cells 5A1 and the B3 comparison) here.

| Source | Fixed 1000-character chunks | Structure-aware chunks | Fixed chunks starting mid-sentence |
|---|---:|---:|---:|
| S01 (PDF) | `<fill in>` | `<fill in>` | `<fill in>` |
| S02 (TXT) | `<fill in>` | `<fill in>` | `<fill in>` |

**Selected method: structure-aware chunking.**
- Split at clause/section headings (`ARTICLE`, `Section N`, numbered headings such as `1. Term`).
- Merge fragments shorter than 80 characters (for example contents-page lines) into the next chunk.
- Split any chunk longer than 3000 characters at blank lines.
- If fewer than three headings are found, fall back to blank-line paragraph blocks.
- Fixed-size chunking is a baseline only. It is simple but cuts clauses mid-sentence and separates a heading from its text.

*Benefit:* each chunk keeps a clause with its heading, which supports FR-05 and traceability (RAI-01, NFR-05).  
*Accepted limitation:* heading detection is rule-based and may split unusual numbering imperfectly. Two contracts are a qualitative sample, not a measured result.

## Extraction and cleaning
- PDF: `pypdf` text extraction, suitable for text-based PDFs.
- TXT: UTF-8 decoding with strict error handling, so encoding problems are surfaced rather than hidden.
- Cleaning: normalise line endings and form feeds, collapse repeated horizontal whitespace, trim excessive blank lines and outer whitespace.
- Headings and clause numbers are preserved because they give context.

## Validation and lineage
- Check source exists and has a supported extension.
- Check extracted and cleaned text are non-empty.
- Check chunks are produced and none is empty.
- Reopen `prepared_text.jsonl` and compare with the in-memory records.
- Run preparation twice and assert identical results.
- Record source filename, SHA-256, prepared-output SHA-256, processing note, dataset, version and licence in `data/week3_manifest.json`, then re-verify the checksums.

## Potential failure points and responses
1. **Scanned/image-only PDF** gives empty or near-empty text. Cell 2 skips PDFs with fewer than 1000 extracted characters and tries the next one. OCR is outside V1.
2. **Missing or unsupported input** raises a clear error before processing.
3. **TXT encoding problems** raise a decoding error instead of silently dropping characters.
4. **Missing headings** trigger the blank-line paragraph fallback.

## Limitations
- Only two contracts were prepared; this demonstrates the pipeline, not clause-detection performance.
- CUAD is commercial contracts, not consumer T&C documents.
- No model is trained in this pipeline, and CUAD labels are not used yet.
- OCR, password-protected PDFs, complex layouts (tables, columns) and multilingual extraction are outside V1.
