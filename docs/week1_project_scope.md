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
