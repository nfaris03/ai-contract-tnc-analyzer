# Week 4 — Data Quality & Bias Report

**Project:** UNCOVER AI — AI-Powered Contract Analysis and Document Review Management System  
**Audit date:** 22 November 2026  
**Decision:** **GO WITH CONDITIONS** for limited, local pipeline development only; **not** clearance for model evaluation, public data redistribution, or deployment.

## 1. Project and Data Overview

UNCOVER AI aims to help users understand contract and Terms & Conditions clauses, with evidence-linked explanations rather than legal advice. This audit covers **FR-05 (Text preparation)**, requiring context-preserving cleaned segments, and **FR-09 (Source display)**, requiring source excerpts and traceability. The relevant Topic 3 pathway is **A — PDF/TXT documents**, Part B prepared output: `data/processed/prepared_text.jsonl` (generated in Google Colab and held locally; **not** published in GitHub). Its matching lineage record is `data/week3_manifest.json`; `data/pipeline_v1/pdf/pipeline_manifest.json` describes the previous run. Source: CUAD v1, one co-branding/advertising agreement in **two formats (PDF and TXT), not two independent contracts**.

**Observed (uploaded current output):** 33 JSONL records, 69,859 bytes; SHA-256 `3b0a0252b64936eda4c99c9910bc5b3e7c57a2473dde37cb003dbfa9d00d5914`; 18 PDF chunks and 15 TXT chunks. The user-reported Colab execution showed JSONL read-back, non-empty chunk, repeatability and source/output checksum-lineage checks as PASS. **Historical GitHub manifest differs:** 69,860 bytes and SHA-256 `628db70cdb428d6e3ca3d1858999c818e812a84cca0bbe8628e880408146aca0`. It refers to an earlier run, not this exact uploaded output. The newly generated manifest was downloaded by the user but has **not** been inspected for this audit.

**Sampling:** 15 of 33 chunks (inspection unit = JSONL record), deliberately selected across both formats and the beginning, middle and end, including fee/payment and termination passages and suspected split-boundary cases. One-based record positions: **1, 2, 5, 7, 8, 9, 10, 11, 13, 15, 19, 24, 28, 29, 33**. This purposive sample is **not statistically representative** of the whole CUAD collection. Automated structural checks also covered all 33 records.

## 2. Five-Dimension Quality Scorecard

| Dimension | Finding and evidence | Potential impact / decision |
|---|---|---|
| **Completeness** | **Observed:** 33/33 records contain all seven expected fields and non-empty text. However, only one agreement was processed; CUAD annotations/labels were not joined. | Basic extraction usable; dataset/category completeness **N.V.**; **Warning** for downstream clause classification. |
| **Consistency** | **Observed:** 33/33 stored `char_count` values equal actual text length. PDF and TXT produce 18 and 15 chunks respectively. | Schema and character-count consistency **Pass**; cross-format segmentation differs and needs review. |
| **Accuracy** | **Observed:** several chunks begin mid-word or mid-sentence (e.g., PDF positions 9 and 11), consistent with maximum-length fallback cuts. The uploaded JSONL was not independently aligned line-by-line with original PDF/TXT files. | Context could be lost at chunk boundaries; source-faithfulness **N.V.**, **Review**. |
| **Timeliness** | **Observed:** source filenames refer to a 1999-era agreement; the dataset is CUAD v1. No task-specific freshness threshold or current consumer-T&C reference was established. | Suitable for a historical pipeline demonstration; suitability for current terms **N.V.**, **Warning**. |
| **Uniqueness** | **Observed:** only 18/33 `chunk_id` values are unique; **15 duplicate ID occurrences** across PDF/TXT. By contrast, all 33 `(source_file, chunk_index)` pairs and all 33 exact text strings are unique. | ID collision could overwrite or confuse retrieval records; **Review / fix before indexing**. |

A duplicated ID is a **metadata defect**, not proof that the PDF and TXT text is identical or should be deleted. Do not discard valid source-format variants automatically.

## 3. Validation Findings

**V1 — FR-05 structural integrity:** Every prepared record must have `source_file`, `source_sha256`, `chunk_id`, `chunk_index`, `method`, `char_count` and non-empty `text`, and `char_count == len(text)`. **Observed:** **33/33 PASS, 0 FAIL**. Action: keep as baseline automated check; separately review boundary accuracy against originals.

**V2 — FR-09 unique evidence identifiers:** `chunk_id` must be unique across the full prepared output, so a future finding can refer unambiguously to its source. **Observed:** **18 distinct IDs across 33 records; 15 duplicate ID occurrences; FAIL**. Example: the PDF's first chunk and TXT's first chunk both have an identifier ending `-001` with the same truncated contract-stem prefix. Action: regenerate identifiers using source format or source hash plus chunk index, then rerun V1/V2 and update manifests. Do not treat `(source_file, chunk_index)` uniqueness as a substitute for the failing standalone ID rule.

These rules were applied directly to the uploaded 33-record JSONL. The reported Colab repeatability check tested deterministic chunking, **not** global identifier uniqueness.

## 4. Duplicate, Anomaly and Coverage Findings

**Duplicate/anomaly:** 15 repeated `chunk_id` occurrences across the two formats, but no exact duplicate text strings (0/33). The differing PDF/TXT chunk counts (18 versus 15) and mid-word/mid-sentence chunk starts require source-level review before retrieval. Cross-format semantic duplication is expected because both formats represent one agreement; it is **not** evidence of 33 independent contracts.

**Coverage check 1 — Payment/fees:** A case-insensitive keyword screen for `payment|fee(s)|compensation|invoice` matched **13/33 records** (7 PDF, 6 TXT); **7/15** sampled records. **Coverage check 2 — Termination/renewal:** `terminate|termination|expire|expiration|renewal|cancel` matched **12/33 records** (6 PDF, 6 TXT); **6/15** sampled records. These are **keyword-presence proxies only**, not verified clause labels, complete category counts or model performance. Manual source/annotation confirmation remains **N.V.**

## 5. Bias Assessment

**Inferred representation bias:** The pipeline selects one historical commercial co-branding agreement from CUAD, while UNCOVER AI intends to help consumers review varied contracts and website Terms & Conditions. **Selection of one agreement → narrow wording/document-type coverage → risk of missing consumer cancellation, renewal, fee or privacy clauses in later detection/explanation → control:** audit additional permitted agreements and consumer T&C examples, and measure per-category coverage with verified labels. Rule-based heading detection and hard 3,000-character cuts also pose **pipeline-induced** context-loss risk. No model fairness or accuracy claim is made.

## 6. Privacy, Rights and Governance

**Provenance:** CUAD v1, The Atticus Project; source PDF/TXT hashes are recorded in the historical `data/week3_manifest.json`. The current uploaded output SHA-256 is recorded above, but **current-output-to-current-manifest correspondence is N.V.** until the newly downloaded manifest is inspected and versioned.

**Permissions:** The CUAD release is described as CC BY 4.0; permission to redistribute each underlying contract or extracted text publicly has **not been verified**. Keep `prepared_text.jsonl` and original contracts outside the public repository pending review. **Privacy:** contract text can contain names, contact details or commercial information; a systematic sensitive-content scan and retention approval are **N.V.** Do not paste raw clauses, personal details or confidential content into GitHub evidence. **Collection/consent basis:** public dataset provenance is documented, but any separate underlying-document consent/rights basis is **N.V.** **Safeguard:** access-restrict local files, share only aggregate counts/checksums, and delete unnecessary copies. The project owner should revalidate on source, pipeline, licence, or schema changes.

## 7. Mitigation and Impact on Requirements

1. **Priority 1 — Before retrieval/indexing (project owner):** Fix global `chunk_id` collisions; inspect boundary cuts against the PDF/TXT originals; regenerate output and both matching manifests, rerun V1/V2 and verify the output SHA-256. Impacts **FR-05** and **FR-09**. Residual risk: headings and source extraction may still be imperfect.
2. **Priority 2 — Before model evaluation or sharing (project owner, with lecturer/authorised reviewer where needed):** Review document-level redistribution permissions/privacy; add diverse permitted consumer T&Cs and agreements; verify category coverage using annotations/manual labels. Impacts **FR-05**, **FR-09** and later **FR-06/FR-07**. Residual risk: commercial/consumer domain shift and incomplete category representation.

## 8. Quality-Gate Decision

**GO WITH CONDITIONS — limited local pipeline development only.** Evidence supporting conditional progress: **(1)** 33/33 records pass the defined structural integrity rule and are non-empty; **(2)** reported Colab read-back/repeatability/checksum checks passed. Conditions preventing an unrestricted GO: **(a)** V2 fails with 15 repeated identifiers; **(b)** only one agreement, in two formats, is represented; **(c)** current manifest match and underlying-document redistribution permissions remain **N.V.** **Do not proceed to production retrieval/indexing, public redistribution, or representative model evaluation** until the two priority actions are completed. Re-review after a corrected 33-record (or expanded) output, a matching current manifest, V1/V2 passes, source-level boundary review, and documented rights/coverage decisions.

---

**Evidence references (safe to share):** `docs/week2_requirements.md` (FR-05, FR-09); `docs/week3_data_inventory.md`; `docs/week3_pipeline_decisions.md`; `notebooks/week3_pipeline.ipynb`; `data/week3_manifest.json` (**historical**); `data/pipeline_v1/pdf/pipeline_manifest.json` (**historical**). Current uploaded `prepared_text.jsonl` was audited locally and is intentionally **not included** in the public repository. Record numbers above are one-based JSONL line positions; no contract text is reproduced here.
