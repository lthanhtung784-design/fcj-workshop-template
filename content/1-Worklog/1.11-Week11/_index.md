---
title: "Week 11 Worklog"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

- Finalize the PhishGuard workshop architecture design and end-to-end incident workflow documentation.
- Build and configure core PhishGuard serverless components (S3 evidence/sanitized buckets, Step Functions approval workflow, and Bedrock synthesis).
- Test incident ingestion, OCR/PII redaction, triage scoring, and SecOps approval callbacks in `DRY_RUN` mode.
- Update workshop documentation on Hugo, verify diagram assets, and prepare the submission.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Finalize the PhishGuard architecture diagram (draw.io, XML, SVG, PNG) and incident flow documentation<br>- Review S3 Object Lock Governance retention, SSE-KMS encryption, and separation between **evidence** and **sanitized** buckets<br>- Define the human-in-the-loop approval callback flow using Step Functions task tokens | 23/11/2026 | 23/11/2026 | AWS Docs – AWS Step Functions Callback Pattern<br>AWS Docs – Amazon S3 Object Lock Overview |
| 2 | - Implement and test the Ingest and Extract & Redact Lambda functions<br>- Verify SHA-256 evidence hashing, Vietnamese/English Tesseract OCR extraction, and PII masking<br>- Validate `NEEDS_MORE_INFO` routing when OCR text and QR indicators are insufficient | 24/11/2026 | 24/11/2026 | AWS Docs – AWS Lambda Developer Guide<br>PhishGuard Workshop Architecture & Implementation Notes |
| 3 | - Configure Triage rule scoring, IOC checks, and Amazon Bedrock playbook synthesis with deterministic fallback<br>- Test `PENDING_APPROVAL`, `NEEDS_REVIEW`, and `NO_ACTION` branching logic<br>- Verify `DRY_RUN` approval execution and audit trail persistence in DynamoDB | 25/11/2026 | 25/11/2026 | AWS Docs – Amazon Bedrock User Guide<br>AWS Docs – Amazon DynamoDB Developer Guide |
| 4 | - Review incident lifecycle states (`NEEDS_MORE_INFO`, `NEEDS_REVIEW`, `NO_ACTION`, `PENDING_APPROVAL`, `REJECTED`, `ESCALATED_TIMEOUT`) and DynamoDB audit records<br>- Verify `DRY_RUN` approval behavior and internal-only blocklist boundaries<br>- Refine bilingual (`en`/`vi`) incident walkthrough text and formatting | 26/11/2026 | 26/11/2026 | AWS Docs – Step Functions `SendTaskSuccess`<br>PhishGuard Workshop Incident Workflow |
| 5 | - Update the Hugo workshop site (`fcj-workshop-template`) with bilingual (`en`/`vi`) PhishGuard pages and architecture diagrams<br>- Fix GitHub Pages subdirectory relative URLs and static asset links<br>- Consolidate Week 11 progress and finalize the workshop submission | 27/11/2026 | 27/11/2026 | Hugo Documentation – URL Management<br>FCAJ Worklog Week 1–11 |

### Week 11 Achievements:

- Completed the end-to-end PhishGuard architecture and incident lifecycle documentation, including downloadable `.drawio`, `.xml`, and `.svg` diagrams.
- Validated evidence integrity (SHA-256, S3 Object Lock), PII redaction, Bedrock playbook synthesis with fallback, and Step Functions human approval callbacks.
- Deployed updated bilingual workshop pages, verified static assets on GitHub Pages, and finalized the submission.