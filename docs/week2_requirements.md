# Week 2 – System Requirements

## 0. Project Framing

**Project:** AI-Powered Contract and Terms & Conditions Analyzer

**Purpose:** Help users locate and understand selected clauses in uploaded contracts and T&C documents through automated text processing, clause categorisation, and plain-language explanations.

**Primary users:** Consumers and general users reviewing agreements.

**System boundary:** The prototype accepts a supported document, extracts text, analyses selected clauses, and displays results. It does not provide legal advice or determine enforceability.

## 1. Functional Requirements

### FR-01: Document upload
The system shall allow a user to upload a supported document format, initially text-based PDF.

### FR-02: File validation
The system shall check whether the uploaded file type and file size are supported and provide a clear error message for unsupported files.

### FR-03: Text extraction
The system shall extract readable text from a supported document.

### FR-04: Extraction feedback
The system shall inform the user when text extraction fails or when the document appears to contain insufficient readable text.

### FR-05: Text preparation
The system shall clean extracted text and divide it into manageable sections or clause segments while preserving enough context for interpretation.

### FR-06: Clause identification
The system shall identify text segments that match the project's selected clause categories.

### FR-07: Clause categorisation
The system shall assign an identified clause to one or more supported categories, such as automatic renewal, fees, cancellation, penalties, liability, and personal data use.

### FR-08: Preliminary attention level
The system shall display a preliminary attention level for identified clauses when supported by the implemented method and evaluation. The interface shall not describe the label as a legal conclusion.

### FR-09: Source display
The system shall display the original clause text or relevant source excerpt alongside each finding.

### FR-10: Plain-language explanation
The system shall provide a simplified explanation for each supported finding and avoid introducing details that are not present in the source.

### FR-11: Analysis summary
The system shall provide a summary of detected clauses and their categories.

### FR-12: No-finding state
The system shall clearly state when no supported clauses are detected and remind the user that this does not prove the document contains no important conditions.

### FR-13: Limitations notice
The system shall display a notice that the tool is an aid for document understanding and is not a substitute for qualified legal advice.

### FR-14: User control
The user shall be able to remove or replace the uploaded document and start a new analysis.

## 2. Non-Functional Requirements

### NFR-01: Usability
The interface should use clear labels, readable text, and a consistent layout suitable for non-specialist users.

### NFR-02: Performance
The system should return analysis results within a practical time for the supported test documents. Processing time will be measured during evaluation.

### NFR-03: Reliability
The system should handle invalid, empty, or unreadable files without crashing and should communicate failures clearly.

### NFR-04: Accuracy
Clause identification and categorisation should be evaluated against a manually labelled test set using appropriate classification metrics.

### NFR-05: Explainability
Each finding should show the source clause and its category. Explanations should be traceable to the supplied document text.

### NFR-06: Privacy
The system should minimise collection and retention of uploaded document data. Test documents should be public or appropriately authorised, and confidential documents should not be used without permission.

### NFR-07: Security
The application should validate uploads, restrict accepted file types and sizes, and avoid exposing uploaded content or internal errors unnecessarily.

### NFR-08: Maintainability
The implementation should separate document processing, clause analysis, explanation generation, and user-interface components where practical.

### NFR-09: Portability
The prototype should be runnable in the documented development environment with clear setup instructions.

### NFR-10: Transparency
The application should explain the meaning and limitations of preliminary attention labels and should not imply legal certainty.

## 3. Responsible AI Requirements

- **RAI-01 – Source grounding:** Every displayed finding must include its supporting source excerpt.
- **RAI-02 – Uncertainty:** The system must communicate when extraction, classification, or explanation is uncertain.
- **RAI-03 – Human oversight:** The interface must encourage users to seek qualified advice for important or unclear matters.
- **RAI-04 – Privacy:** Uploaded files and extracted text must be handled with appropriate access and retention controls.
- **RAI-05 – Fair evaluation:** Testing should include different document structures and clause wording where suitable data is available.
- **RAI-06 – Avoid misleading claims:** The system must not claim that a contract is legally valid, invalid, fair, unfair, or safe based only on automated output.

## 4. Proposed System Components

1. User interface and document upload.
2. File validation and PDF text extraction.
3. Text cleaning and clause segmentation.
4. Clause identification and classification.
5. Preliminary attention-level assignment.
6. Plain-language explanation generation.
7. Results and analysis summary.
8. Privacy, error handling, and limitations notices.

## 5. Proposed Technology Options

- Python for application and NLP logic.
- Streamlit for the prototype interface.
- PDF text extraction library for supported PDF documents.
- Scikit-learn for baseline classification experiments.
- NLP models or an LLM for explanation generation, subject to feasibility and evaluation.
- Pandas and NumPy for data preparation and analysis.

These are proposed options, not a claim that all components have already been implemented.

## 6. Requirement Traceability

- FR-01 to FR-04 support document input and extraction.
- FR-05 to FR-08 support clause preparation, detection, and categorisation.
- FR-09 to FR-13 support understandable and responsible results.
- FR-14 supports user control.
- NFR-04 and NFR-05 support measurable accuracy and traceability.
- NFR-06, NFR-07, and RAI-04 address privacy and security.
- RAI-01 to RAI-06 address grounded, transparent, and responsible output.

## 7. Assumptions and Open Questions

- The initial version targets English text-based PDF documents.
- The final list of clause categories depends on data availability and project evaluation.
- A labelled dataset or manually annotated sample set will be needed for meaningful evaluation.
- The use of external LLM services, if any, must be reviewed for cost, privacy, and data-handling implications.
- OCR and multilingual processing are not guaranteed in the initial scope.
