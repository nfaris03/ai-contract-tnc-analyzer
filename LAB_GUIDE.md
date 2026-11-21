# START HERE — UNCOVER AI Repository Guide

This guide explains **where everything is**, **what each lab does**, and **what is still missing**. Read it before opening individual files.

> **Important:** A written requirement is a *plan*, not a finished feature. The Week 3 manifest describes a prior local pipeline run; the public notebook has no saved execution outputs. The AI clause classifier, dashboard and review-management system are not yet demonstrated as working.

## The three labs in one minute

| Lab | Main question | What you produce |
|---|---|---|
| **Topic 1 / Lab 1** | **What problem am I solving, and why?** | Problem statement, users, objectives, existing work, project scope, conceptual system map |
| **Topic 2 / Lab 2** | **What should the system do, and how will I evaluate/design it?** | Requirements (FR/NFR/RAI), metrics, architecture, decisions |
| **Topic 3 / Lab 3** | **How do I get usable contract text and prove where it came from?** | Dataset inventory, PDF/TXT pipeline notebook, preparation comparison, validation and lineage |
| **Topic 4** | **Not started in this repository guide** | Read Topic 4 instructions before creating files |

## Lab 1 — Project scoping

| File | Why you open it |
|---|---|
| [docs/week1_project_scope.md](docs/week1_project_scope.md) | **Main submission:** problem, evidence, research, objectives, users, scope, public sources, risks, EduAdvisor comparison |
| [docs/week1_observation_sheet.md](docs/week1_observation_sheet.md) | Group activity output: problem observation; does **not** claim completed interviews |
| [docs/week1_system_map.md](docs/week1_system_map.md) | Editable Mermaid description of actors and their interactions |
| `docs/week1_system_map.png` | **Required PNG not yet verified in repository** |

**To verify:** student-authored reflection; actual comparison to lecturer's EduAdvisor manual; PNG export; Moodle URL; repo naming convention.

## Lab 2 — Requirements, architecture, evaluation

| File | Why you open it |
|---|---|
| [docs/week2_requirements.md](docs/week2_requirements.md) | **Part A:** FR (functions), NFR (quality), Responsible AI |
| [docs/week2_evaluation_criteria.md](docs/week2_evaluation_criteria.md) | **Part B:** how to measure quality; thresholds are proposed, not achieved |
| [docs/week2_architecture_v1.md](docs/week2_architecture_v1.md) | Editable Mermaid architecture source |
| [docs/week2_architecture_decisions.md](docs/week2_architecture_decisions.md) | **Part C:** component choices, trade-offs and traceability supplement |
| `docs/week2_architecture_v1.png` | **Required PNG not yet verified in repository** |

**To verify:** PNG export, reflections, Moodle URL. **FR** = what it must do; **NFR** = how well; **RAI** = responsible AI safeguards.

## Lab 3 — Data engineering

| File | Why you open it |
|---|---|
| [docs/week3_data_inventory.md](docs/week3_data_inventory.md) | **Part A:** dataset identity, source inspection and access considerations |
| [notebooks/week3_pipeline.ipynb](notebooks/week3_pipeline.ipynb) | **Part C:** Python notebook to ingest, inspect, clean, chunk, validate and record lineage |
| [docs/week3_pipeline_decisions.md](docs/week3_pipeline_decisions.md) | **Parts B/C:** why PDF/TXT, chunking comparison, limitations and failure handling |
| [docs/week3_pipeline_diagram.svg](docs/week3_pipeline_diagram.svg) | Existing visual workflow in SVG format |
| `docs/week3_pipeline_diagram.png` | **Required PNG not yet verified in repository** |
| [data/week3_manifest.json](data/week3_manifest.json) | **Part B:** historical local-run source/output metadata and hashes |
| [data/pipeline_v1/pdf/pipeline_manifest.json](data/pipeline_v1/pdf/pipeline_manifest.json) | **Part C:** historical local-run execution summary |
| [data/processed/synthetic_demo.jsonl](data/processed/synthetic_demo.jsonl) | Clearly **synthetic illustration**, **not** the output of the CUAD pipeline |

**To verify:** run the notebook with the authorized CUAD source, save Cell 9 repeatability evidence, create the required executed outputs and PNG; confirm the lecturer's preferred secure submission method for contract-derived text. The two source files inspected are PDF/TXT formats of **one** agreement.

## Folder map

```text
README.md                      <- HOME PAGE: open this first
LAB_GUIDE.md                   <- YOU ARE HERE: explanation of every lab
docs/                          <- Written lab reports + diagrams
  week1_*                      <- Lab 1
  week2_*                      <- Lab 2
  week3_*                      <- Lab 3
  uncover_ai_scope_extension.md<- Planned FYP/extra product features
data/                          <- Source metadata and prepared outputs
  week3_manifest.json          <- Lab 3 common lineage
  processed/                   <- Lab 3 prepared data; synthetic demo only in public repo
  pipeline_v1/pdf/             <- Lab 3 pipeline manifest
notebooks/                     <- Lab 3 executable Python notebook
src/                           <- Reserved for future application code
evaluation/                    <- Reserved for future AI model evaluation
prompts/                       <- Reserved for future prompt assets, if used
```

## How Lab 3 data moves

`CUAD archive -> choose PDF/TXT pair -> extract text -> clean text -> split into chunks -> save JSONL -> validate -> record SHA-256 lineage`

- **Ingestion:** read the original files.
- **Extraction:** obtain text from PDF/TXT.
- **Cleaning:** normalize text artifacts.
- **Chunking:** split long text into manageable passages.
- **Validation:** check nonempty output and JSONL reload.
- **Lineage:** track source files, processing choices and checksums.
- **Repeatability:** confirm the same inputs/settings produce the same prepared chunks.

**No trained clause detection model is demonstrated by this data pipeline.**

## What belongs to AI Engineering versus the FYP extension?

**Core AI Engineering project:** PDF input, text preparation, clause detection/classification, source-grounded explanation, evaluation and responsible-AI controls.

**Additional proposed product features:** document library, dashboard, review status/notes, PDF report export, user accounts and SQLite storage. See [the separate extension](docs/uncover_ai_scope_extension.md). These are **planned**, not evidence that the labs implemented them.

## Remaining submission checklist

- [ ] Export and commit `docs/week1_system_map.png`.
- [ ] Export and commit `docs/week2_architecture_v1.png`.
- [ ] Export and commit `docs/week3_pipeline_diagram.png`.
- [ ] Execute Lab 3 notebook yourself and capture Cell 9 output; verify repeatability.
- [ ] Agree on rights-safe actual prepared-output submission with lecturer.
- [ ] Add genuine personal reflections to relevant lab files.
- [ ] Verify Moodle URL submissions and repository accessibility.
- [ ] Check whether lecturer requires the exact `ai-engineering-[name]` repository naming convention.

## Recommended reading order

1. This guide.
2. Lab 1 project scope.
3. Lab 2 requirements -> evaluation criteria -> architecture.
4. Lab 3 inventory -> notebook -> decisions -> manifests.
5. Only then read the FYP scope extension or start Lab 4.
