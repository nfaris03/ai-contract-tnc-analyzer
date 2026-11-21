# Week 1 – Project Scope

## 1. Project Title

AI-Powered Contract and Terms & Conditions Analyzer

## 2. Problem Background

Contracts, service agreements, and Terms & Conditions (T&C) documents explain the conditions that users accept when subscribing to services, purchasing products, registering for platforms, or entering into agreements. These documents may contain important information about fees, automatic renewal, cancellation, penalties, liability, and personal data.

However, users may not read the documents carefully because they are lengthy, use formal or complex language, or take time to review. Important conditions may therefore be overlooked or misunderstood. This project focuses on helping users locate and understand selected clauses; it does not assume that every clause is harmful or legally unfair.

## 3. Problem Statement

Users may find it difficult and time-consuming to identify important contractual conditions in lengthy documents and understand their practical meaning. Manually reviewing every clause can require considerable effort, particularly for people without legal knowledge. There is a need for an accessible document-analysis tool that can extract relevant clauses, organise them into understandable categories, and explain why they may deserve further attention.

## 4. Proposed Solution

Develop a web-based application that allows users to upload supported contract or T&C documents. The system will extract the text, identify clauses belonging to selected review categories, and present the original clause with a plain-language explanation and a preliminary attention level.

The application will provide information to support a user's own review. It will not provide legal advice, decide whether a clause is enforceable, or guarantee detection of every important condition.

## 5. Project Objectives

1. To develop an AI-powered application for analysing uploaded contract and T&C documents.
2. To apply NLP and machine learning techniques to identify and categorise selected contractual clauses.
3. To generate clear, source-grounded explanations of selected clauses in plain language.
4. To evaluate clause identification, classification, explanation quality, and processing time.

## 6. Target Users and Stakeholders

- **Consumers and general users:** People who need help understanding online service terms, subscriptions, or agreements.
- **Students and young adults:** Users who may encounter rental, service, subscription, or purchase agreements.
- **Small business owners and freelancers:** Users who review service agreements or business terms but may not have immediate access to legal support.
- **Legal professionals and reviewers:** Potential secondary users who may use the output as an initial document-navigation aid, not as a replacement for professional judgement.
- **Developers and project team:** Responsible for building, testing, and maintaining the application.

## 7. Initial Scope

The initial prototype will focus on:
- Uploading supported text-based PDF documents.
- Extracting and preparing document text.
- Splitting extracted text into clauses or manageable text segments.
- Identifying selected clause categories, such as automatic renewal, fees, cancellation, penalties, liability, and personal data use.
- Assigning preliminary review labels such as High, Medium, or Low, subject to evaluation.
- Showing the original text alongside a plain-language explanation.
- Displaying a concise analysis summary.

## 8. Out of Scope

The initial prototype will not:
- Provide formal legal advice or legal representation.
- Determine whether a contract is legally valid or enforceable.
- Guarantee that all risky or important clauses will be detected.
- Automatically accept, reject, sign, or negotiate an agreement for the user.
- Replace review by a qualified legal professional.
- Support every language, file format, or scanned document in the initial version.

OCR for scanned PDFs and multilingual support may be considered only if time and project resources allow.

## 9. Initial Clause Categories

The initial categories proposed for investigation are:
- Automatic renewal and subscription continuation.
- Additional, recurring, or unexpected fees.
- Cancellation and termination conditions.
- Late-payment charges and penalties.
- Limitation or exclusion of liability.
- Personal data collection, use, and sharing.
- User obligations, permissions, and restrictions.

These categories are a starting scope and may be refined after reviewing public documents and preparing an annotated evaluation dataset.

## 10. Existing Solutions and Research Review Plan

The project should compare at least three relevant existing solutions, research studies, or document-analysis approaches. The review should record:
- Name and purpose of the solution or study.
- Type of documents or clauses addressed.
- AI/NLP methods used, where documented.
- Main capabilities.
- Limitations relevant to this project.

No performance claims or conclusions should be added until the original sources have been checked. The engineering gap should be written from the comparison, rather than assumed in advance.

## 11. Proposed Data Sources

Potential public data sources for the project include:
- Publicly available Terms & Conditions and privacy-policy documents published by online services.
- Public sample contracts and agreement templates made available for educational or informational use.
- Public research datasets or benchmark corpora containing legal or contractual text, if their licence and suitability can be verified.

For each source, record its URL, publisher, document type, access date, licence or usage conditions, and intended use. A minimum of two to three suitable public document sources should be identified and checked before they are used for model development or evaluation. Public availability does not automatically mean unrestricted reuse.

## 12. Responsible AI Risks

- **Incorrect detection:** The system may miss relevant clauses or flag ordinary clauses incorrectly.
- **Misleading explanations:** Generated summaries may omit exceptions or change the meaning of the original clause.
- **False confidence:** Users may treat a preliminary risk label as a legal conclusion.
- **Privacy and confidentiality:** Uploaded contracts may contain personal, financial, or confidential information.
- **Bias and coverage:** Performance may vary across document types, writing styles, jurisdictions, and languages.
- **Copyright and data rights:** Public documents may have restrictions on copying, storing, or redistributing their contents.

Mitigations include displaying the original clause, grounding explanations in extracted text, communicating uncertainty, limiting data retention, testing across document types, and clearly stating that the tool is not legal advice.

## 13. Success Criteria

The project will be considered successful at prototype level if it can:
- Process supported sample documents and extract readable text.
- Identify and categorise the selected clause types against a labelled test set.
- Display the original text for each detected clause.
- Produce explanations that human evaluators judge clear and faithful to the source.
- Report evaluation metrics and processing time transparently.

Numerical performance targets will be set in the Week 2 evaluation plan after the dataset and annotation approach are defined.

## 14. Initial Assumptions and Constraints

- The first prototype will prioritise English-language, text-based documents.
- The project will use public or appropriately authorised documents for development and evaluation.
- Clause labels and severity labels will require a documented annotation guideline.
- The final model and interface technologies will be selected based on feasibility and evaluation results.
- The system is an educational decision-support prototype, not a legal service.

## 15. Current Status

Week 1 establishes the problem, target users, objectives, scope, candidate clause categories, data-source plan, and Responsible AI considerations. Existing-solution research and data-source selection must be supported by checked sources before final submission.


---

## UNCOVER AI — Additive Project Extension (Planned)

**Updated proposed title:** UNCOVER AI: An AI-Powered Contract Analysis and Document Review Management System.

The existing AI contract/T&C analyzer remains the **core FYP component**: upload text-based PDFs, extract and prepare text, identify and categorize clauses, provide plain-language explanations, and show the supporting original excerpts. The application is now intended for **both individuals and organizational users**.

**Additional planned supporting features:**
- **Dashboard:** counts of total documents, pending review, reviewed, user-approved, and needs-attention documents; recent uploads; and a chart of detected clause categories.
- **My Documents:** saved document and analysis history, search/filter, reopen, and deletion.
- **Review Management:** user-controlled review statuses and notes, tracked separately from AI findings or processing status.
- **PDF Reports:** export identified clauses, supporting source excerpts, explanations, and limitations.
- **Basic accounts and storage:** user-specific access and document metadata/analysis persistence (SQLite proposed for the prototype).

**Important:** These are proposed additions, **not implemented or evaluated features**. An 'approved' status is a user's workflow decision, not an AI legal-safety judgment. AI-generated attention indicators must not be presented as legal conclusions. Existing lecturer lab activities and reported results remain unchanged. See [UNCOVER AI scope extension](uncover_ai_scope_extension.md) for details.

**Scope priority:** AI analysis and evaluation first; document dashboard and review workflow second. Team approvals, chatbot, and contract comparison are outside the initial scope.


## Week 1 completion supplement — evidence, related work and public examples (22 Nov 2026)

### Evidence of the problem (secondary evidence, not a user survey)
- The Atticus Project's CUAD research frames contract review as locating important provisions in long agreements. Its 510 commercial contracts and 13,000+ expert annotations across 41 clause types demonstrate the breadth of the identification task: https://www.atticusprojectai.org/cuad/ ; Hendrycks et al. (2021), https://arxiv.org/abs/2103.06268 . This is evidence that automated clause identification is an active research problem, **not** evidence of a measured problem among UNCOVER AI's intended consumers.
- Terms of Service; Didn't Read (ToS;DR) exists to make online terms easier to understand through community-reviewed points and ratings: https://tosdr.org/en . Its existence motivates the use case but does not independently quantify how many people misunderstand terms.

### Three existing approaches and limitations
| Existing work | What it does | Limitation relevant to UNCOVER AI |
|---|---|---|
| CUAD / Hendrycks et al. (2021), https://arxiv.org/abs/2103.06268 | Expert-annotated benchmark for locating important clauses in commercial agreements | Dataset and benchmark, not a ready-to-use consumer document review application; commercial-contract coverage may not transfer to consumer T&C. |
| ToS;DR, https://tosdr.org/en | Volunteer-reviewed summaries and ratings of service terms and privacy policies | Depends on community-reviewed service coverage; not the same as analyzing each arbitrary PDF uploaded by a user. |
| Fouché (2024), study of Lawgeex contract review in practice, https://hdl.handle.net/10539/45135 | Empirical study comparing an automated contract-review platform with human reviewers | Focuses on a specific organizational contract-review setting, not validation of consumer T&C explanations or UNCOVER AI's six categories. |

### Engineering gap
A small, evaluable prototype is needed that accepts a user-provided text PDF, identifies a limited set of important clauses, displays original evidence with plain-English explanations, and supports human-controlled review history. This is a **proposed project gap**, not a claim that no commercial system provides such features.

### Two specific publicly accessible example documents
1. Google Terms of Service — Google, https://policies.google.com/terms (public HTML, PDF download offered; use as a candidate for authorized inspection, not automatically as redistributable training data).
2. Google Privacy Policy — Google, https://policies.google.com/privacy (public HTML; candidate for inspection of data-use wording; check reuse restrictions and format before processing).

CUAD v1 is a separate research dataset source: https://www.atticusprojectai.org/cuad/ . Public visibility does not grant unrestricted rights to redistribute document text.

### Comparison with lecturer's EduAdvisor example
**Similarity:** Both are user-facing AI decision-support concepts that collect input, process it, present an understandable result and must communicate uncertainty. **Difference:** EduAdvisor concerns educational guidance and recommendations, while UNCOVER AI processes unstructured contractual PDF text, locates source clauses, and presents evidence-linked explanations. The exact EduAdvisor architecture/feature list must be checked against the Topic 1 manual; this comparison is conceptual only.

### Scope clarification
Initial AI Engineering objectives are (1) prepare and validate supported contract text, (2) detect/classify selected clauses, and (3) provide evidence-grounded explanations and evaluate the prototype. Dashboard and review management are supporting planned functions, not completed AI features.

### Reflection prompt for the student
Before submission, write 2–3 sentences in your own words: which example contract you inspected, what surprised you, and why you selected this scope. Do not present invented interviews or observations as personal work.
