# Week 3 – Data Inventory

## Project context
**Project:** AI-Powered Contract and Terms & Conditions Analyzer  
**Selected pathway:** PDF and TXT document ingestion.

## Source pack
The supplied `Topic_3_Dummy_Datasets.zip` README states that all examples are synthetically generated for teaching and that the pack is a practice fallback, not a replacement for the dataset justified by Topic 2.

### 1. student_handbook_demo.pdf
- Format: text-based PDF; document identifies itself as “2026 Demo Edition” and lists “Teaching Team” as owner.
- Purpose: demonstrate PDF text extraction, inspection, cleaning and section-aware chunking.
- Inspection: 1 page; 426 extracted characters; title/metadata followed by four sections: Registration, Attendance, Graduation and Academic Support.
- Observation: short illustrative statements; no real institutional policy and no contract clauses.
- Access/use: supplied in the synthetic teaching ZIP; lab use only.
- SHA-256: `3dc6270e4a2d072afe07502c27c0bb71a2305bf2e020f01cc86fe96d7950ec5e`

### 2. faq_demo.txt
- Format: UTF-8 plain text.
- Version/date and owner: not stated.
- Purpose: demonstrate TXT ingestion and preservation of FAQ question-and-answer blocks.
- Inspection: 171 bytes; 170 characters after cleaning; two Q&A pairs.
- Observation: questions concern course information and graduation rules; answers direct readers to the course catalogue and faculty office.
- Access/use: supplied in the synthetic teaching ZIP; lab use only.
- SHA-256: `05461ed704d8c8cf8b7a609e2b4b4e7cb800a7fe16a68fe5805546a7b3e2f43f`

## Inspection observations
- PDF text extraction returned selectable text; OCR was not needed for this sample.
- PDF section headings provide useful chunk boundaries.
- Blank lines separate the TXT FAQ pairs, allowing each Q&A pair to remain together.
- Both samples are small and synthetic.

## Project relevance and limitation
These files exercise basic document-ingestion mechanics relevant to the planned upload feature. They are not project-domain contract data and cannot support claims about clause detection, legal-risk classification or model accuracy. A permission-checked contract dataset or authorized sample agreements must be selected separately for later AI development and evaluation.

## Scope decision
Only PDF/TXT is implemented because it matches the current document-upload workflow. Tabular, image, JSON/API, audio and time-series pathways in the ZIP are outside the current project scope.
