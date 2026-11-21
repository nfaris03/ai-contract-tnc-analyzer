# UNCOVER AI
**AI-Powered Contract Analysis and Document Review Management System**  
*Understand Before You Agree*

> **New here? Read [LAB_GUIDE.md](LAB_GUIDE.md) first.** It explains the folder structure, the purpose of each file and what is still incomplete.

## Project in simple English

UNCOVER AI is a proposed AI-assisted tool that helps people understand contracts and Terms & Conditions. A user uploads a supported text-based PDF; the intended system extracts text, identifies selected clause types, and presents plain-language explanations alongside the original wording. It is a decision-support prototype, **not legal advice**.

**Problem:** Important contract terms can be lengthy and hard to locate or understand.  
**Engineering gap:** A small, measurable document-analysis workflow with evidence-linked findings, transparent limitations and human review.  
**Target users:** Individuals, students, small businesses and other document reviewers.

**Main objectives:** (1) prepare supported contract text; (2) identify and categorize relevant clauses using evaluated NLP/ML; (3) explain findings with original evidence and evaluate accuracy and usability.

**Initial clause categories:** automatic renewal, cancellation/termination, fees, penalties, limitation of liability, and personal-data use.

**Evidence and related work:** [CUAD research](https://arxiv.org/abs/2103.06268), [ToS;DR](https://tosdr.org/en), and a third related-work comparison are discussed in the [Lab 1 project scope](docs/week1_project_scope.md). These references motivate the problem; they are not results from user interviews.

**Candidate data:** [CUAD](https://huggingface.co/datasets/theatticusproject/cuad), [Google Terms](https://policies.google.com/terms), and [Google Privacy Policy](https://policies.google.com/privacy). Check usage rights before copying or redistributing content.

## Go directly to your lab

| Topic | What it is about | Open this first |
|---|---|---|
| **Lab 1 — Project scope** | Why this project, who needs it and what is in scope | [Week 1 project scope](docs/week1_project_scope.md) |
| **Lab 2 — Requirements and design** | Features, quality requirements, architecture and proposed metrics | [Week 2 requirements](docs/week2_requirements.md) |
| **Lab 3 — Data engineering** | CUAD PDF/TXT preparation, checks and lineage | [Week 3 data inventory](docs/week3_data_inventory.md) |
| **Lab 4 — Upcoming** | Not yet documented | Wait for lecturer instructions |

**Every file explained:** [LAB_GUIDE.md](LAB_GUIDE.md).

## Weekly progress — documented versus verified

| Week | Documented work | Important outstanding items |
|---|---|---|
| **1** | Problem, users, scope, risk, research/source supplement | PNG system map, personal reflection, Moodle check |
| **2** | FR/NFR/RAI, evaluation plan, architecture decisions and traceability | PNG architecture, personal reflection |
| **3** | CUAD inventory, pipeline notebook, chunking comparison, historical local-run manifests | PNG pipeline, independently rerun Cell 9, authorized executed outputs |
| **4** | Not started | Await lab instructions |

## How the planned system works

`Upload PDF -> validate -> extract text -> clean and segment -> detect/classify clauses -> generate grounded explanations -> show results`

**Current evidence:** Lab 3 documentation reports one matched PDF/TXT agreement, 9 PDF pages, 33 prepared chunks and a successful *historical local* validation/repeatability run. These are not model-accuracy results, and the GitHub notebook has no saved execution outputs.

**Proposed technologies:** Python, Streamlit, pypdf, scikit-learn, optional evaluated LLM for explanations. Model selection and performance remain to be established.

**Proposed evaluation targets (not achieved):** clause identification F1 ≥ 0.75, category macro-F1 ≥ 0.70, human explanation rating ≥ 4/5, valid-document processing ≥ 90%, and typical processing time ≤ 30 seconds.

## Responsible AI

Display original evidence, acknowledge missed clauses and uncertainty, protect uploaded documents, and avoid making legal judgments. Consumer T&C coverage is not established by CUAD commercial-contract data. OCR and multilingual support are outside the first version.

## FYP / future additions

The [UNCOVER AI scope extension](docs/uncover_ai_scope_extension.md) describes **planned** dashboard, document library, user review statuses, PDF reports and accounts/storage. These features are separate from evidence of what Labs 1–3 completed.

## Repository layout

- `docs/`: Week 1–3 written lab deliverables and diagrams
- `notebooks/`: Lab 3 pipeline notebook
- `data/`: Lab 3 manifests and authentic CUAD category metadata and historical pipeline manifests
- `src/`: reserved for future app code
- `evaluation/`: reserved for future model evaluation
- `prompts/`: reserved for future prompts, if used

**Submission note:** The original lecturer-required filenames remain unchanged. Check [the remaining-work checklist](LAB_GUIDE.md#remaining-submission-checklist) before claiming all labs complete.
