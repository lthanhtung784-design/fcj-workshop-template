---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

- Understand logging and investigation with CloudTrail.
- Detect threats with GuardDuty and send alerts via EventBridge/SNS.
- Assess configuration compliance with Security Hub.
- Learn web application protection with AWS WAF, Macie, and Firewall Manager.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study AWS CloudTrail: Event history vs trails, management events vs data events<br>- Understand that CloudTrail data events are not logged by default and need extra configuration<br>- Learn log file validation and delivering logs to a dedicated bucket<br>- Practice lookup-events to find activity by access key or user | 19/10/2026 | 19/10/2026 | AWS Cloud Journey – S3 Security Best Practices<br>AWS Docs – AWS CloudTrail User Guide<br>AWS Docs – Logging data events |
| 2 | - Study the module Threat Detection with AWS GuardDuty<br>- Enable GuardDuty and S3 Protection; learn finding types (for example Exfiltration:S3/AnomalousBehavior)<br>- Generate sample findings to observe results without simulating a real attack<br>- Connect GuardDuty → EventBridge → SNS → Email and test the alerting flow | 20/10/2026 | 20/10/2026 | AWS Cloud Journey – Threat Detection with AWS GuardDuty<br>AWS Docs – Amazon GuardDuty User Guide<br>AWS Docs – Generating sample findings |
| 3 | - Study the module Security Compliance with AWS Security Hub<br>- Enable Security Hub with the AWS Foundational Security Best Practices standard<br>- Read findings, severity levels, and the compliance score<br>- Note pricing considerations and disable the service after practice | 21/10/2026 | 21/10/2026 | AWS Cloud Journey – Security Compliance with AWS Security Hub<br>AWS Docs – AWS Security Hub User Guide |
| 4 | - Study the module Application Protection with AWS WAF<br>- Learn web ACLs, managed rule groups, and rate-based rules<br>- Use Count mode to test rules before switching to Block<br>- Identify WAF limits: it does not replace secure coding and application patching | 22/10/2026 | 22/10/2026 | AWS Cloud Journey – Application Protection with AWS WAF<br>AWS Docs – AWS WAF Developer Guide |
| 5 | - Study the module Data Protection with Amazon Macie<br>- Learn how Macie detects sensitive data (PII) in S3<br>- Study the module Security Governance with AWS Firewall Manager<br>- Understand centralized WAF and Security Group management through AWS Organizations; note pricing | 23/10/2026 | 23/10/2026 | AWS Cloud Journey – Data Protection with Amazon Macie<br>AWS Cloud Journey – Security Governance with AWS Firewall Manager<br>AWS Docs – Amazon Macie User Guide<br>AWS Docs – AWS Firewall Manager |

### Week 6 Achievements:

- Distinguished the role of each service: CloudTrail (who did what), GuardDuty (anomalous behavior), Security Hub (configuration compliance), WAF (web request filtering).
- Built an alert flow GuardDuty → EventBridge → SNS → Email using sample findings.
- Understood that data events must be configured to investigate object-level activity.
- Learned to assess costs and disable billable services after practice.
- Understood that a finding does not necessarily mean a compromise and evidence must be checked first.