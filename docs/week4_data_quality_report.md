# Week 4 — Data Quality & Bias Report

**Project:** UNCOVER AI — AI-Powered Contract Analysis and Document Review Management System  
**Audit date:** 22 November 2026  
**Decision:** **GO WITH CONDITIONS** for limited, local pipeline development only; **not** clearance for model evaluation, public data redistribution, or deployment.

## 1. Project and Data Overview

UNCOVER AI aims to help users understand contract and Terms & Conditions clauses, with evidence-linked explanations rather than legal advice. This audit covers **FR-05 (Text preparation)**, requiring context-preserving cleaned segments, and **FR-09 (Source display)**, requiring source excerpts and traceability. The relevant Topic 3 pathway is **A — PDF/TXT documents**, Part B prepared output: `data/processed/prepared_text.jsonl` (generated in Google Colab and held locally; **not** published in GitHub). Its matching lineage record is `data/week3_manifest.json`; `data/pipeline_v1/pdf/pipeline_manifest.json` describes the previous run. Source: CUAD v1, one co-branding/advertising agreement in **two formats (PDF and TXT), not two independent contracts**.

**Observed (uploaded current output):** 33 JSONL records, 68,638 bytes; SHA-256 `8fd6866e435e29d43bb0f2c115d179ac0edef9a9b27e0adf4c83627b34d753fa`; 18 PDF chunks and 15 TXT chunks. The user-reported Colab execution showed JSONL read-back, non-empty chunk, repeatability and source/output checksum-lineage checks as PASS. **Verified current manifest:** the user-supplied Colab manifest generated **2026-11-22T13:05:56.124399+00:00** reports **33 records**, **68,638 bytes**, and SHA-256 `8fd6866e435e29d43bb0f2c115d179ac0edef9a9b27e0adf4c83627b34d753fa`. Independent comparison of the uploaded JSONL confirmed exact size, record count, and SHA-256. The public `data/week3_manifest.json` has now been updated to describe this corrected run; the 11 November manifest was historical.

**Sampling:** 15 of 33 chunks (inspection unit = JSONL record), deliberately selected across both formats and the beginning, middle and end, including fee/payment and termination passages and suspected split-boundary cases. One-based record positions: **1, 2, 5, 7, 8, 9, 10, 11, 13, 15, 19, 24, 28, 29, 33**. This purposive sample is **not statistically representative** of the whole CUAD collection. Automated structural checks also covered all 33 records.

## 2. Five-Dimension Quality Scorecard

| Dimension | Finding and evidence | Potential impact / decision |
|---|---|---|
| **Completeness** | **Observed:** 33/33 records contain all seven expected fields and non-empty text. However, only one agreement was processed; CUAD annotations/labels were not joined. | Basic extraction usable; dataset/category completeness **N.V.**; **Warning** for downstream clause classification. |
| **Consistency** | **Observed:** 33/33 stored `char_count` values equal actual text length. PDF and TXT produce 18 and 15 chunks respectively. | Schema and character-count consistency **Pass**; cross-format segmentation differs and needs review. |
| **Accuracy** | **Observed:** several chunks begin mid-word or mid-sentence (e.g., PDF positions 9 and 11), consistent with maximum-length fallback cuts. The uploaded JSONL was not independently aligned line-by-line with original PDF/TXT files. | Context could be lost at chunk boundaries; source-faithfulness **N.V.**, **Review**. |
| **Timeliness** | **Observed:** source filenames refer to a 1999-era agreement; the dataset is CUAD v1. No task-specific freshness threshold or current consumer-T&C reference was established. | Suitable for a historical pipeline demonstration; suitability for current terms **N.V.**, **Warning**. |
| **Uniqueness** | **Observed:** **33/33 `chunk_id` values are unique; 0 duplicate ID occurrences** after correcting the source-specific ID generation. The initial audit found 18 distinct IDs and 15 duplicate ID occurrences; this defect has been fixed and revalidated. All 33 `(source_file, chunk_index)` pairs and exact text strings are also unique. | **Pass** for ID uniqueness; cross-format semantic overlap still needs handling before indexing. |

A duplicated ID is a **metadata defect**, not proof that the PDF and TXT text is identical or should be deleted. Do not discard valid source-format variants automatically.

## 3. Validation Findings

**V1 — FR-05 structural integrity:** Every prepared record must have `source_file`, `source_sha256`, `chunk_id`, `chunk_index`, `method`, `char_count` and non-empty `text`, and `char_count == len(text)`. **Observed:** **33/33 PASS, 0 FAIL**. Action: keep as baseline automated check; separately review boundary accuracy against originals.

**V2 — FR-09 unique evidence identifiers:** `chunk_id` must be unique across the full prepared output, so a future finding can refer unambiguously to its source. **Initial audit:** 18 distinct IDs across 33 records, 15 duplicate ID occurrences (**FAIL**). **Correction:** changed the chunk-ID generation from the truncated contract stem to the complete source filename (`p.name`) plus chunk index; retained all 33 records. **Final revalidation of the uploaded corrected JSONL:** **33 distinct IDs / 33 records, 0 duplicate occurrences, PASS**. For future multi-document use, include a stable source hash or other globally unique source identifier. Do not treat `(source_file, chunk_index)` uniqueness as a substitute for the failing standalone ID rule.

These rules were applied directly to the uploaded 33-record JSONL. The reported Colab repeatability check tested deterministic chunking, **not** global identifier uniqueness.

## 4. Duplicate, Anomaly and Coverage Findings

**Duplicate/anomaly:** The initial 15 repeated `chunk_id` occurrences have been corrected: **0 duplicate IDs** in the final 33-record output, and no exact duplicate text strings (0/33). The differing PDF/TXT chunk counts (18 versus 15) and mid-word/mid-sentence chunk starts require source-level review before retrieval. Cross-format semantic duplication is expected because both formats represent one agreement; it is **not** evidence of 33 independent contracts.

**Coverage check 1 — Payment/fees:** A case-insensitive keyword screen for `payment|fee(s)|compensation|invoice` matched **13/33 records** (7 PDF, 6 TXT); **7/15** sampled records. **Coverage check 2 — Termination/renewal:** `terminate|termination|expire|expiration|renewal|cancel` matched **14/33 records** in the corrected uploaded output; the previously stated sample and per-format breakdown were not rerun and are **N.V.** for this corrected version. These are **keyword-presence proxies only**, not verified clause labels, complete category counts or model performance. Manual source/annotation confirmation remains **N.V.**

## 5. Bias Assessment

**Inferred representation bias:** The pipeline selects one historical commercial co-branding agreement from CUAD, while UNCOVER AI intends to help consumers review varied contracts and website Terms & Conditions. **Selection of one agreement → narrow wording/document-type coverage → risk of missing consumer cancellation, renewal, fee or privacy clauses in later detection/explanation → control:** audit additional permitted agreements and consumer T&C examples, and measure per-category coverage with verified labels. Rule-based heading detection and hard 3,000-character cuts also pose **pipeline-induced** context-loss risk. No model fairness or accuracy claim is made.

## 6. Privacy, Rights and Governance

**Provenance:** CUAD v1, The Atticus Project; source PDF/TXT hashes are recorded in the historical `data/week3_manifest.json`. The corrected uploaded output's byte length and SHA-256 **match the user-supplied Colab manifest (independently verified)**, and the current public GitHub manifest has been replaced with the corresponding verified metadata. Original source-file hashes are recorded in the manifest but were not independently recalculated from the underlying PDF/TXT in this audit.

**Permissions:** The CUAD release is described as CC BY 4.0; permission to redistribute each underlying contract or extracted text publicly has **not been verified**. Keep `prepared_text.jsonl` and original contracts outside the public repository pending review. **Privacy:** contract text can contain names, contact details or commercial information; a systematic sensitive-content scan and retention approval are **N.V.** Do not paste raw clauses, personal details or confidential content into GitHub evidence. **Collection/consent basis:** public dataset provenance is documented, but any separate underlying-document consent/rights basis is **N.V.** **Safeguard:** access-restrict local files, share only aggregate counts/checksums, and delete unnecessary copies. The project owner should revalidate on source, pipeline, licence, or schema changes.

## 7. Mitigation and Impact on Requirements

1. **Priority 1 — Before retrieval/indexing (project owner):** **Completed:** fixed global `chunk_id` collisions, regenerated output and matching manifest, and verified V1/V2 and SHA-256. **Still required:** inspect boundary cuts against the PDF/TXT originals and ensure the corrected notebook is committed to GitHub. Impacts **FR-05** and **FR-09**. Residual risk: headings and source extraction may still be imperfect.
2. **Priority 2 — Before model evaluation or sharing (project owner, with lecturer/authorised reviewer where needed):** Review document-level redistribution permissions/privacy; add diverse permitted consumer T&Cs and agreements; verify category coverage using annotations/manual labels. Impacts **FR-05**, **FR-09** and later **FR-06/FR-07**. Residual risk: commercial/consumer domain shift and incomplete category representation.

## 8. Quality-Gate Decision

**GO WITH CONDITIONS — limited local pipeline development only.** Evidence supporting conditional progress: **(1)** 33/33 records pass the defined structural integrity rule and are non-empty; **(2)** reported Colab read-back/repeatability/checksum checks passed. Conditions preventing an unrestricted GO: **(a)** only one agreement, in two formats, is represented; **(b)** source-text fidelity and chunk-boundary accuracy remain **N.V.**; **(c)** underlying-document redistribution permissions and privacy review remain **N.V.** **Do not proceed to production retrieval/indexing, public redistribution, or representative model evaluation** until the two priority actions are completed. The corrected 33-record output, matching current manifest and V1/V2 passes are now verified. Re-review after source-level boundary inspection, broader category/document coverage, and documented rights/privacy decisions.

---

**Evidence references (safe to share):** `docs/week2_requirements.md` (FR-05, FR-09); `docs/week3_data_inventory.md`; `docs/week3_pipeline_decisions.md`; `notebooks/week3_pipeline.ipynb`; `data/week3_manifest.json` (**current verified metadata**); user-supplied **corrected Colab manifest** generated 2026-11-22 13:05 UTC (SHA-256/size/record count verified); `data/pipeline_v1/pdf/pipeline_manifest.json` (**historical**). Current uploaded `prepared_text.jsonl` was audited locally and is intentionally **not included** in the public repository. Record numbers above are one-based JSONL line positions; no contract text is reproduced here.
