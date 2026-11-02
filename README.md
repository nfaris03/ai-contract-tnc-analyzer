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

## Proposed workflow
1. Document upload and file validation.
2. PDF text extraction.
3. Text cleaning and clause segmentation.
4. Clause identification and categorisation.
5. Preliminary attention-level assignment.
6. Source-grounded explanation generation.
7. Results presentation with source excerpts and limitations notice.

## Proposed technologies
Python, Streamlit, PDF extraction libraries, NLP/ML methods, Pandas, NumPy, and Scikit-learn. An LLM may be considered for explanations subject to feasibility, privacy, and evaluation.

## Responsible AI and limitations
- Show the original source excerpt for every finding.
- Communicate uncertainty and extraction failures.
- Protect uploaded documents and avoid unnecessary retention.
- Do not claim legal validity, invalidity, fairness, or enforceability.
- Encourage human review and qualified legal advice for important matters.

## Topic 3 – Data ingestion and preparation

**Selected dataset:** CUAD v1 (Contract Understanding Atticus Dataset), a real, expert-annotated collection of commercial contracts. Dataset source: https://huggingface.co/datasets/theatticusproject/cuad. Citation: Hendrycks et al. (2021), CUAD: An Expert-Annotated NLP Dataset for Legal Contract Review, arXiv:2103.06268.

**Selected pathway:** PDF/TXT document ingestion. The notebook is designed to download two representative CUAD contracts, inspect them, compare fixed-size and structure-aware chunking, export prepared text, and create checksum-based lineage records.

### Topic 3 files
- Data inventory: docs/week3_data_inventory.md
- Pipeline notebook: notebooks/week3_pipeline.ipynb
- Pipeline decisions: docs/week3_pipeline_decisions.md
- Common data manifest: data/week3_manifest.json
- Pipeline manifest: data/pipeline_v1/pdf/pipeline_manifest.json

**Status: Notebook prepared; execution and evidence pending.** Run the notebook in Google Colab, inspect the selected contracts, and replace the pending manifest with actual generated outputs and checksums. No CUAD contract files or prepared outputs are currently committed. The former lecturer dummy files have been removed from the Lab 3 data folders.

CUAD focuses on commercial contracts, not consumer-style website T&C documents. The two-contract pipeline sample demonstrates ingestion and preparation only; it does not establish clause-detection accuracy. Review the dataset licence and the terms applicable to individual underlying documents before redistributing contract files.
