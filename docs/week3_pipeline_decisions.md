# Week 3 – Pipeline Decisions

## Selected pathway
PDF and TXT document ingestion, aligned with the document-upload workflow in the Topic 2 architecture.

## Preparation comparison

| Source | Structure-aware chunks | Fixed 160-character chunks |
|---|---:|---:|
| student_handbook_demo.pdf | 5 | 3 |
| faq_demo.txt | 2 | 2 |

**Selected method: structure-aware chunking.**
- PDF: preserve the opening title/metadata and begin a new chunk at each `Section N:` heading.
- TXT: preserve each blank-line-separated FAQ question-and-answer block.
- Fixed-size chunking is a baseline only. It is simple but can split headings, sentences or Q&A pairs at arbitrary character positions.

The samples are small, so this is a qualitative engineering decision, not a statistically proven performance result.

## Extraction and cleaning
- PDF: PyMuPDF text extraction; appropriate for the supplied text-based PDF.
- TXT: UTF-8 decoding.
- Cleaning: normalize line endings, collapse repeated horizontal whitespace, trim excessive blank lines and outer whitespace.
- Preserve section headings and FAQ labels because they provide context.

## Validation and lineage
- Check source existence and supported extension.
- Check extracted and cleaned text are non-empty.
- Check chunks are produced.
- Reopen each saved JSON output and compare chunks with the in-memory result.
- Record source filename, byte size, SHA-256, extraction method, preparation method and output path.
- Run preparation twice and assert identical results.

## Potential failure points and responses
1. Scanned/image-only PDF may produce empty text. Detect this and report OCR is required; OCR is outside V1.
2. Missing or unsupported input should trigger a clear error before processing.
3. TXT encoding problems should be surfaced rather than silently dropping characters.

## Limitations
- Samples are synthetic teaching examples, not real contracts.
- They do not validate clause identification or legal-risk classification.
- No model is trained in this pipeline.
- OCR, password-protected PDFs, complex layouts and multilingual extraction are outside V1.
- Larger and varied contract documents must be tested later.
