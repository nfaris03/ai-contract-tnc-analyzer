# AI-Powered Contract and Terms & Conditions Analyzer

## Project overview
This project proposes an AI-based application that helps users understand contracts and Terms & Conditions documents before accepting or signing them. It aims to extract document text, identify selected clauses that may need attention, and explain those clauses in plain language with the original text as evidence.

The system supports document understanding only. It does not determine legal validity, fairness, or enforceability and does not replace professional legal advice.

## Problem and proposed solution
Contracts and T&C documents can be lengthy and contain complex wording. Users may overlook important conditions such as fees, automatic renewal, cancellation restrictions, penalties, liability limitations, and personal-data use.

The proposed web application will accept a supported document, extract and prepare its text, identify clauses matching selected review categories, and display the original clause with a plain-language explanation and preliminary attention label.

## Objectives
1. Develop an AI-powered application for analysing uploaded contracts and T&C documents.
2. Apply NLP/ML techniques to identify and categorise selected clauses.
3. Generate plain-language explanations grounded in the source text.
4. Evaluate clause identification, classification, explanation quality, and processing time.

## Proposed technologies
Python, Streamlit, PDF extraction libraries, NLP/ML methods, Pandas, NumPy, and Scikit-learn. An LLM may be considered for explanations subject to feasibility, privacy, and evaluation.

## Responsible AI and limitations
- Show the original source excerpt for every finding.
- Communicate uncertainty and extraction failures.
- Protect uploaded documents and avoid unnecessary retention.
- Do not claim legal validity, invalidity, fairness, or enforceability.
- Encourage human review and qualified legal advice for important matters.

## Topic 3 – Data ingestion and preparation

**Selected dataset:** CUAD v1 (Contract Understanding Atticus Dataset), a real, expert-annotated collection of commercial contracts. Dataset source: https://huggingface.co/datasets/theatticusproject/cuad. Research citation: Hendrycks et al. (2021), *CUAD: An Expert-Annotated NLP Dataset for Legal Contract Review*, arXiv:2103.06268.

**Selected pathway:** PDF/TXT document ingestion. The pipeline inspected a matched PDF/TXT pair for one CUAD agreement, extracted text, compared fixed-size and structure-aware chunking, exported prepared JSONL locally, and generated source/output lineage metadata.

### Topic 3 files
- Data inventory: docs/week3_data_inventory.md
- Pipeline notebook: notebooks/week3_pipeline.ipynb
- Pipeline decisions: docs/week3_pipeline_decisions.md
- Pipeline diagram (SVG): docs/week3_pipeline_diagram.svg
- Common data manifest: data/week3_manifest.json
- Pipeline run manifest: data/pipeline_v1/pdf/pipeline_manifest.json

### Execution evidence
- Source PDF: 9 pages; 29,376 extracted characters.
- Matched TXT: 29,454 characters; strict UTF-8 read succeeded.
- Structure-aware chunks: 18 from PDF and 15 from TXT (33 total).
- Prepared JSONL: 69,860 bytes; reload validation passed.
- Repeatability and SHA-256 lineage checks passed.

**Important sample limitation:** the PDF and TXT are two formats of the same agreement, not two independent contracts. This is a pipeline demonstration, not representative dataset evaluation or clause-detection accuracy testing.

**Data handling:** raw contract files and prepared_text.jsonl are excluded from this public repository because redistribution rights for individual underlying contracts and extracted text must be checked. The manifest records filenames, checksums and processing evidence without publishing contract text. The notebook includes a Colab upload workflow; the successful execution recorded in the manifest was performed in a local Python/Jupyter kernel, not in the student's Colab account.

CUAD focuses on commercial contracts, not consumer-style website T&C documents. Consumer T&C coverage, OCR, multilingual processing, model training and clause-detection evaluation remain future work.
