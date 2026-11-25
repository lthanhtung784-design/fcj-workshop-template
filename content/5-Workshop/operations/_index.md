---
title: "5.6 · Well-Architected review"
weight: 6
chapter: false
---

Open a demo incident, its Step Functions execution and the authorized S3 evidence version. These answer three different questions: what the analyst saw, which path the workflow took and which original object it processed. Record the time, incident ID and version ID together. Use the same evidence to examine the design against AWS Well-Architected.

| Criterion | Decision in PhishGuard | Verification and limits |
|---|---|---|
| Architecture and deployment (0.5) | CloudFront has a web ACL. Web and SES submissions converge at Ingest. Raw evidence is saved before the workflow starts. Step Functions owns the approval callback. | Compare the behaviors, receipt rule, SAM template and one execution with the arrows in 5.1. Lambda uses AWS-managed networking. The template defines no application subnet. |
| Operational Excellence (0.5) | Review change sets before updates. Two alarms notify the SecOps topic about failed executions and Ingest DLQ depth. | In 5.5.1 inspect alarm state, actions and topic ARN. Trace a notification timestamp to its execution or Ingest log. An OK screenshot records the state at capture time. |
| Security (0.5) | The API validates JWTs and checks roles. Raw evidence has a separate SSE-KMS bucket with versioning and seven-day Governance retention. Approval goes through Admin API. | Run H02 and H15 with two reporters and an auditor. Compare ordinary and marked GETs in the WAF test. Direct S3 POSTs are governed by the signed policy and Ingest validation. Restrict Governance bypass privileges. |
| Reliability (0.5) | Ingest uses request identity for retries and routes exhausted asynchronous invocations to a DLQ. The workflow handles approval expiry and synthesis can fall back. | Exercise H01/H04 and H13/H14 on the demo. For a DLQ message check the cause, incident and raw version before reprocessing. This deployment is single-region. Recovery time and recovery point for a regional outage have not been measured. |
| Performance Efficiency (0.5) | Direct upload keeps file bytes out of the HTTP API. Image extraction uses 512 MiB x86_64 Lambda with OCR and QR support. The preparation Lambda returns while the workflow waits for the reviewer. | Compare p50/p95 Duration, Billed Duration and Max Memory Used for image and text cohorts with known sizes. Inspect Throttles and measure human approval latency separately. Benchmarks remain open. |
| Cost Optimization (0.5) | The model separates report counts, image processing, AI calls and fixed service costs. WAF is the largest line at 300 reports per month. | Recalculate the CSV in 5.7, change one assumption and compare with billing for the matching period. Identify shared fees such as the hosted zone and charges that outlive the lab. |
| Sustainability (recorded, 0 points) | Event-driven processing and an intake lifecycle limit time and storage spent on temporary work. | Check lifecycle rules and older versions after the exercise. Retain evidence through its promised retention period. Workload emissions have not been measured. |

### Responding to an alarm

If the DLQ depth alarm fires, record the timestamp and request ID. Find the asynchronous Ingest invocation in CloudWatch Logs. Check access to the source object and required write permissions. Look up the incident, evidence version and execution before retrying a lab event. After recovery, verify the expected number of incidents and executions, confirm that the raw version remains accessible and retain the log explaining the initial failure.

### Explaining the architecture in a review

Choose a connection that is easy to misread, such as a direct upload or an approval callback. Open its configuration and explain the caller, destination, data and failure behavior. Describe your own contribution to the AI-assisted diagram accurately and retain its revision history if available. Mark design targets, observations and estimates clearly when presenting evidence.

[AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/the-pillars-of-the-framework.html) · [FCAJ workshop rubric](https://hcm-rules.awsfcaj.com/scoring/workshop)
