# Lab 3 data — CUAD v1

This repository uses the **real Contract Understanding Atticus Dataset (CUAD) v1** from The Atticus Project.

## What is actually committed here?

- [raw/cuad_category_descriptions.csv](raw/cuad_category_descriptions.csv): **authentic category metadata** copied from the official CUAD repository's `category_descriptions.csv` (not synthetic).
- [week3_manifest.json](week3_manifest.json): manifest describing an earlier local PDF/TXT processing run.
- [pipeline_v1/pdf/pipeline_manifest.json](pipeline_v1/pdf/pipeline_manifest.json): summary of the earlier local run.
- `processed/`: expected destination for prepared JSONL; actual CUAD contract-text output is **not yet committed**.

**The category CSV is part of the genuine CUAD dataset, but does not contain the 510 contracts.** It is not a substitute for running the PDF/TXT pipeline.

## Download the full actual CUAD dataset

Official publisher: https://www.atticusprojectai.org/cuad/

Official source code and archive: https://github.com/The-Atticus-Project/cuad

Official CUAD release: https://zenodo.org/records/4595826

Download the CUAD v1 ZIP from the publisher and use the existing [Lab 3 notebook](../notebooks/week3_pipeline.ipynb), which prompts for the archive in Colab. The archive includes contract PDFs/TXTs and annotations; do **not** upload the entire ~106 MB archive to GitHub just to satisfy Lab 3.

The official CUAD release is licensed **CC BY 4.0**; the dataset's own datasheet notes that it makes no warranties about the underlying contracts' license status. Attribute the publisher and verify any intended redistribution. Source: https://huggingface.co/datasets/theatticusproject/cuad/blob/main/CUAD_v1/CUAD%20v1%20ReadMe%20_%20Datasheet/CUAD_v1_README.txt

## Important

A previously reported run inspected one PDF/TXT pair representing **one agreement**, not all 510 contracts. Re-run the notebook and record actual outputs and Cell 9 repeatability evidence before claiming the full pipeline has been reproduced.

Citation: Hendrycks, D., Burns, C., Chen, A., & Ball, S. (2021). *CUAD: An Expert-Annotated NLP Dataset for Legal Contract Review*. NeurIPS. https://arxiv.org/abs/2103.06268
