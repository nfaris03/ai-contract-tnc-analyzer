# UNCOVER AI — Project Scope Extension (Addendum)

> **Additive document only.** This file records the agreed FYP extensions. It does not replace or revise the existing Week 1–3 lecturer lab submissions, dataset artifacts, architecture decisions, or evaluation plans. Features described below are **planned**, not implemented or tested.

## 1. Updated product identity

**Product name:** UNCOVER AI

**Proposed FYP title:** UNCOVER AI: An AI-Powered Contract Analysis and Document Review Management System

**Primary contribution remains:** AI-assisted contract and Terms & Conditions clause identification, categorisation, plain-language explanations, and original-source evidence.

**Supporting contribution:** Document review management and an overview dashboard.

The existing pipeline, CUAD dataset choice, selected clause categories, text-based PDF focus, Streamlit prototype approach, and evaluation strategy remain in place.

## 2. Intended users

- **Individuals:** Review documents such as rental agreements, employment contracts, and Terms & Conditions before agreeing to them; save their findings and track what they have reviewed.
- **Organizational users:** Review and track multiple contracts, such as supplier or service agreements, through their own accounts.

**Initial organizational scope:** A company user can manage their own document collection. Shared company workspaces, team roles, manager approvals, and multi-stage approval workflows are **not included** in the initial extension.

## 3. Proposed additional modules

### 3.1 Dashboard

Display summaries computed from stored documents and user review decisions:

- Total uploaded documents
- Documents awaiting user review
- Reviewed documents
- User-approved documents
- Documents marked as needing attention
- Recent documents and analysis results
- Counts of detected clause categories (optional chart)

**Important distinction:** An AI finding or attention indicator is separate from a user-set review status. User approval does **not** mean the AI has determined legal safety, fairness, or enforceability.

### 3.2 My Documents

- List previously uploaded and analysed documents
- Search and filter by document name, date, or review status
- Reopen stored analysis results and source excerpts
- Delete documents and associated stored data, subject to the implemented retention policy

### 3.3 Review management

- Track document states, for example: Uploaded -> Analysed -> Pending Review -> Reviewed / Approved / Needs Attention
- Allow users to manually change review status and add notes
- Store the last review update time
- Treat status labels as **user workflow decisions**, not legal conclusions

### 3.4 Exportable analysis report

Generate a downloadable PDF report containing:

- Document identifier/name and analysis date
- Identified clause categories
- Relevant original excerpts and source references where available
- Plain-language explanations
- Preliminary attention indicators only if implemented and evaluated
- Limitations and non-legal-advice notice

### 3.5 Accounts and privacy (proposed)

- Basic user authentication
- Keep each user's document history and review records separate
- Restrict access to stored uploaded files, extracted text, and analysis results
- Define retention and deletion behavior; avoid storing sensitive contract text unnecessarily

## 4. Additional functional requirements (supplement to Week 2 FR-01–FR-14)

These are **new** requirements; existing requirement IDs remain unchanged.

- **FR-15 — Document persistence:** The system shall store document metadata and analysis results needed for later review.
- **FR-16 — Dashboard:** The system shall display counts of documents grouped by user-controlled review status and recent activity.
- **FR-17 — Document library:** The system shall allow users to list, search, filter, reopen, and delete their own saved documents.
- **FR-18 — Review status:** The system shall allow users to set and update a document's review status independently of AI findings.
- **FR-19 — Review notes:** The system shall allow users to attach notes to a document review.
- **FR-20 — PDF report:** The system shall allow users to export an analysis report containing findings, supporting evidence, and limitations.
- **FR-21 — User access:** If accounts are implemented, the system shall restrict document and review access to the authorized user.

## 5. Proposed data model (extension only)

A simple relational database (e.g., SQLite for a prototype) may store:

- **users:** user ID and authentication metadata
- **documents:** document ID, owner ID, filename, upload timestamp, processing state, retention metadata
- **analysis_results:** document ID, analysis timestamp, model/version information, summary, processing status
- **clause_findings:** result ID, category, source excerpt, source location if available, explanation, optional attention indicator
- **reviews:** document ID, reviewer ID, user-set review status, notes, updated timestamp

Document processing status (uploaded, processing, analysed, failed) should be tracked **separately** from user review status (pending, reviewed, approved, needs attention), so dashboard totals are not ambiguous.

## 6. Scope boundaries and development priority

**Core / first priority:** Existing extraction and NLP pipeline; baseline clause identification and classification; grounded explanations; evidence display; appropriate evaluation.

**Supporting / second priority:** Document persistence, dashboard, document library, user review statuses, and notes.

**Third priority:** PDF export and basic authentication/privacy controls, as feasible for the FYP timeline. If persistence is enabled, access control and secure retention/deletion must be designed before handling real confidential contracts.

**Future work, not committed:** Team approvals, organization-wide shared workspaces, contract comparison, chatbot Q&A, OCR, multilingual analysis, and advanced risk scoring.

## 7. Evaluation extension

**Keep the existing Week 2 evaluation criteria for the AI component.** Add separate system-level tests for:

- Correct dashboard counts and review status transitions
- Saving and reopening analyses without losing source evidence
- Search, filter, note-taking, deletion, and PDF report export
- Account isolation and protection of stored documents, if accounts are enabled
- Usability of the dashboard and review workflow for both individuals and organizational users

The current CUAD-based preparation work is a pipeline demonstration, **not** proof of clause-model accuracy. CUAD focuses on commercial contracts; additional authorized consumer-style T&C examples may be needed to assess performance for individual users.

## 8. Relationship to existing lecturer labs

This addendum supplements, without changing, the existing:
- `README.md`
- `docs/week1_*.md`
- `docs/week2_*.md`
- `docs/week3_*.md` and diagram
- `notebooks/week3_pipeline.ipynb`
- `data/` artifacts and manifests

The existing architecture remains the analyzer pipeline. The proposed dashboard and review-management components connect **after** results assembly and use stored analysis results; they must not replace or bypass the analyzer.

**Status:** Planning / proposed scope extension. No claim is made here that these additional features have been built.
