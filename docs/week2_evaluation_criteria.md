# Week 2 – Evaluation Criteria

## 1. Evaluation Purpose

The evaluation will measure whether the AI-Powered Contract and Terms & Conditions Analyzer can identify selected clauses, assign useful categories, provide understandable explanations, and process supported documents reliably.

The system must be evaluated against a labelled test set. Results should not be based only on a few successful demonstrations.

## 2. Evaluation Dataset

The proposed evaluation dataset should contain public or appropriately authorised contract and T&C documents.

Preparation steps:
1. Collect documents from documented sources and record their URLs, publishers, access dates, and reuse conditions.
2. Select documents that represent the intended scope and supported document format.
3. Divide documents into clause-level segments.
4. Create annotation guidelines defining each clause category and examples.
5. Label relevant clauses manually. Where possible, use a second reviewer to check a subset and resolve disagreements.
6. Split data into training, validation, and test sets at document level to reduce leakage between clauses from the same document.
7. Keep the test set separate from model development and tuning.

The dataset size and category distribution must be reported after collection. Do not claim a dataset size or annotation agreement score before measuring it.

## 3. Metrics

### 3.1 Clause identification

Measure precision, recall, and F1-score.

- **Precision:** Of the clauses flagged by the system, how many are relevant?
- **Recall:** Of the relevant clauses in the labelled test set, how many did the system find?
- **F1-score:** The harmonic mean of precision and recall.

Recall is important because missed clauses may matter, while precision is important because too many irrelevant alerts may reduce user trust.

### 3.2 Clause classification

Measure per-category precision, recall, and F1-score, together with macro-F1. Report a confusion matrix where appropriate. Macro-F1 helps show performance across categories rather than allowing frequent categories to dominate the result.

### 3.3 Explanation quality

Use human evaluation with a documented rubric. Reviewers should assess:
- Faithfulness to the original clause.
- Clarity and readability.
- Completeness of important conditions and exceptions.
- Whether the explanation adds unsupported claims.
- Whether the source excerpt supports the explanation.

Use a rating scale, such as 1 (poor) to 5 (excellent), and report the number of examples and reviewers. Human ratings should not be represented as objective legal correctness.

### 3.4 Processing performance

Measure end-to-end processing time from document submission to displayed results. Report the number and type of test documents, average time, and, where practical, median and maximum time.

### 3.5 Reliability

Record:
- Successful extraction rate.
- Number of failed or unreadable documents.
- Invalid-file handling.
- Whether the application completes analysis without crashing.

## 4. Initial Acceptance Targets

The following are proposed prototype targets for planning. They are not achieved results and should be reviewed after a pilot test and dataset preparation.

- Clause identification: target F1-score of at least 0.75 on the held-out test set.
- Clause classification: target macro-F1 of at least 0.70.
- Explanation quality: average human rating of at least 4 out of 5 for faithfulness and clarity.
- Reliability: successfully process at least 90% of valid supported test documents.
- Performance: aim to complete analysis of a typical supported document within 30 seconds in the documented test environment.

If the dataset is too small or imbalanced to support these targets, report the limitation and justify revised thresholds rather than manipulating the test set.

## 5. Test Scenarios

- Valid text-based PDF containing known target clauses.
- Valid PDF containing no clauses from the selected categories.
- PDF with long sections and multiple clauses.
- PDF with unusual formatting or broken text extraction.
- Unsupported file type.
- Empty or unreadable document.
- Clause with an exception or qualifying condition.
- Similar wording used in a different context.
- Document containing personal or confidential information (use synthetic or authorised test material).

## 6. Evaluation Reporting

The final report should include:
- Dataset sources and selection criteria.
- Number of documents and clause segments.
- Category distribution.
- Annotation process and limitations.
- Train/validation/test split method.
- Model or baseline configuration.
- Precision, recall, F1-score, and confusion matrix.
- Human explanation-evaluation rubric and results.
- Processing-time measurements.
- Error analysis with examples of false positives and false negatives.
- Limitations and planned improvements.

## 7. Responsible Evaluation

A model should not be considered successful solely because it produces fluent explanations. Explanations must be checked against source clauses. Evaluation should include missed findings, incorrect alerts, unsupported statements, and user misunderstanding risks. Automated outputs must remain advisory and should not be presented as legal conclusions.
