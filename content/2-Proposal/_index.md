---
title: "2. Project proposal"
weight: 2
chapter: false
---

**PhishGuard AI · Omnichannel phishing triage with human approval**  
Proposed pilot: an internal security operations team and employees reporting suspicious messages. Deployment region: US East (N. Virginia). The demo runs containment in `DRY_RUN`.

## The operational problem

An employee forwards a suspicious message to a general mailbox. A second employee reports an image of the same campaign. The analyst needs to identify each reporter, preserve precisely what each person submitted, explain a recommendation and find the decision later. Copying text into a chatbot helps with interpretation. Someone still has to connect the evidence, access controls, reviewer and outcome.

## What the pilot delivers

A Cognito-authenticated portal accepts pasted text, screenshots and EML files. An SES receiving rule accepts forwarded email from verified reporters. Ingest gives each report an incident ID and preserves a version of the original. Analysts use a redacted copy for routine work. A separate, audited request gives a privileged analyst short-lived access to the original.

The policy engine computes the score from indicators and named rules. Bedrock can retrieve playbooks and explain the result. If generation fails, the analyst still sees the rule result and the fallback reason. Where an action is proposed, Step Functions records a deadline, notifies SecOps and resumes only on a valid decision or a timeout. Approval records retain the human decision. A simulated block, a confirmed entry in the internal list and enforcement by an external product have different operational effects. External enforcement is outside the pilot.

## Deliverables and acceptance

| Milestone | Deliverable | How to accept it |
|---|---|---|
| Intake and preservation | Portal, SES and separate evidence stores | Submit a UTF-8 message and an image, then trace an incident to its S3 version. Repeating the same reporter request returns its incident. |
| Analysis | OCR, PII masking, policy evaluation and grounded summary | Inspect the extracted Vietnamese text, triggered rules and evidence. Low-quality input asks for more information. Record the actual synthesis status. |
| Approval | Admin decision, callback and audit log | An approved demo produces an audit record. An unanswered request expires. A late decision returns HTTP 409. |
| Operations and handover | Role-specific reads, alarms, workshop and cost model | A second reporter cannot read the first reporter’s incident. Demonstrate alarm targets, a reproducible deployment and the assumptions behind cost. |

## Boundaries and risks

Object Lock Governance protects a raw version for seven days subject to authorized bypass. OCR may miss accents and masking can leave names or addresses. Forwarded headers describe the original message as supplied by the employee. SES authentication proves facts about the outer delivery. Analysts must interpret those separately. False-positive and false-negative rates on unseen real-world messages still require a labelled evaluation set.

**Deployed scope.** The CloudFront distribution has the PhishGuardEdge web ACL. Raw uploads go directly to S3. Image extraction supports Vietnamese/English OCR and URL QR codes. Five source playbooks support retrieval. Triage proposes eligible actions and Bedrock explains them.

## Costs and pilot decision

For a 30-day month with 300 reports, 90 images and 60 inbound emails, the model estimates **USD 9.37**, including the permanent WAF rules and one hosted zone. The Cost Explorer report for 1–23 November 2026 rounds to **USD 0.00** within its export scope. Before extending the pilot, compare time to triage, false alerts, missed cases and manual review against the current mailbox process using an independently labelled set.

![Deployed architecture]({{< asset "images/phishguard/architecture-final.png" >}})

[Architecture walkthrough](../5-workshop/overview/) · [Cost model and billing evidence](../5-workshop/cost/)
