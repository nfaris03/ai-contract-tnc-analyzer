# Week 2 – System Requirements

## 0. Project Framing

**Project:** AI-Powered Contract and Terms & Conditions Analyzer

**Purpose:** Help users locate and understand selected clauses in uploaded contracts and T&C documents through automated text processing, clause categorisation, and plain-language explanations.

**Primary users:** Consumers and general users reviewing agreements.

**System boundary:** The prototype accepts a supported document, extracts text, analyses selected clauses, and displays results, with a dashboard and authorised document review management. It does not provide legal advice or determine enforceability.

## 1. Functional Requirements

- **FR-01 – Document upload and processing:** Accept, validate and extract readable text from supported text-based PDFs within configured size limits; clean and segment text while retaining context.
- **FR-02 – Clause identification and classification:** Detect relevant segments and assign one or more supported categories (renewal, fees, cancellation, penalties, liability, personal data).
- **FR-03 – Attention assessment:** Display preliminary High/Medium/Low labels only where supported by evaluation; not legal conclusions.
- **FR-04 – Explanation and source display:** Show original excerpts, source-grounded plain-language explanations and a summary of detected clauses and categories.
- **FR-05 – Dashboard:** Show saved document totals, detected category and attention distributions, and review progress.
- **FR-06 – Document management:** Save authorised analyses, list names, dates, summaries and detailed findings; filter by document, category and review status; remove or replace uploads, start new analyses and delete saved content and associated counts.
- **FR-07 – Review status:** Allow user-set Pending, Reviewed and Completed statuses for documents or findings and persist changes.
- **FR-08 – Error handling:** Clearly report unsupported or oversized files, failed or insufficient extraction and no findings; clarify that no findings does not establish safety.

## 2. Non-Functional Requirements

- **NFR-01 – Performance:** Measure end-to-end latency; proposed p90 ≤30 seconds for defined supported test files.
- **NFR-02 – Accuracy and data quality:** Evaluate detection and classification against held-out labelled data (proposed F1 ≥0.75 and macro-F1 ≥0.70); verify source identifiers, structural validity and exact dashboard totals against stored records.
- **NFR-03 – Reliability:** Handle ≥95% of predefined error cases and review workflows; preserve saved statuses after restart.
- **NFR-04 – Usability:** Clear labels, readable text and consistent navigation; proposed mean clarity ≥4/5 and ≥80% dashboard task completion.
- **NFR-05 – Maintainability and portability:** Separate processing, analysis, explanation and UI modules; document setup and rerun steps.

## 3. Responsible AI Requirements

- **RAI-01 – Transparency and explainability:** Every finding includes its source excerpt; explanations must be grounded (proposed ≥90% faithful); dashboard counts represent detected findings only.
- **RAI-02 – Privacy and security:** Minimise collection and retention; use authorised documents, restrict access, validate file type and size, avoid exposing content or internal errors, and verify deletion of associated records.
- **RAI-03 – Human oversight and limitations:** Communicate extraction, classification and explanation uncertainty; label attention levels preliminary; display no-finding caveats and non-legal-advice notice; encourage qualified advice for important or unclear matters.
- **RAI-04 – Fair and responsible evaluation:** Test varied document structures and wording where suitable data exists; never claim legal validity, fairness or safety solely from automated output.

## 4. Proposed System Components

1. User interface and document upload.
2. File validation and PDF text extraction.
3. Text cleaning and clause segmentation.
4. Clause identification and classification.
5. Preliminary attention-level assignment.
6. Plain-language explanation generation.
7. Results and analysis summary.
8. Privacy, error handling, and limitations notices.
9. Dashboard, authorised document library, filters, deletion and review status.

## 5. Proposed Technology Options

- Python for application and NLP logic.
- Streamlit for the prototype interface.
- PDF text extraction library for supported PDF documents.
- Scikit-learn for baseline classification experiments.
- NLP models or an LLM for explanation generation, subject to feasibility and evaluation.
- Pandas and NumPy for data preparation and analysis.

These are proposed options, not a claim that all components have already been implemented.

## 6. Requirement Traceability

- FR-01 and FR-08: input, extraction, preparation and error feedback.
- FR-02–04: clause analysis, attention assessment and evidence-linked results.
- FR-05–07: dashboard, document management and review workflow.
- NFR-01–05: performance, quality, reliability, usability and maintainability.
- RAI-01–04: grounding, privacy/security, human oversight and fair evaluation.

Historical Topic 4 references to the previous FR-05 (preparation) and FR-09 (source display) now correspond to FR-01 and FR-04 respectively. Historical audit results remain unchanged.

## 7. Assumptions and Open Questions

- The initial version targets English text-based PDF documents.
- The final list of clause categories depends on data availability and project evaluation.
- A labelled dataset or manually annotated sample set will be needed for meaningful evaluation.
- The use of external LLM services, if any, must be reviewed for cost, privacy, and data-handling implications.
- OCR and multilingual processing are not guaranteed in the initial scope.
