---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

- Master advanced IAM policies: conditions and permission evaluation logic.
- Understand IAM Permission Boundaries for delegation without privilege escalation.
- Use AWS SSO (IAM Identity Center) instead of long-term IAM users.
- Understand encryption with KMS and secrets management with Secrets Manager.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study the module Access Control with IAM Policies and Conditions<br>- Learn policy evaluation logic: default deny, explicit deny always wins<br>- Practice conditions aws:MultiFactorAuthPresent, aws:SourceIp, and aws:RequestedRegion<br>- Test with the Policy Simulator and record cases where a permission exists but access is still denied | 12/10/2026 | 12/10/2026 | AWS Cloud Journey – Access Control with IAM Policies and Conditions<br>AWS Docs – Policy evaluation logic<br>AWS Docs – Security best practices in IAM (<https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html>) |
| 2 | - Study the module Permission Management with IAM Permission Boundaries<br>- Understand the privilege-escalation risk of allowing role/user creation<br>- Create a permission boundary, attach it to a delegated user, and compare behavior before and after<br>- Summarize the relationship between identity policies, boundaries, and SCPs | 13/10/2026 | 13/10/2026 | AWS Cloud Journey – Permission Management with IAM Permission Boundaries<br>AWS Docs – Permissions boundaries for IAM entities |
| 3 | - Study the module Identity Federation with AWS Single Sign-On<br>- Learn IAM Identity Center, permission sets, and group-based assignments<br>- Sign in to the CLI with SSO (aws configure sso) and compare it with long-term access keys<br>- Evaluate the security benefits: temporary credentials and centralized MFA | 14/10/2026 | 14/10/2026 | AWS Cloud Journey – Identity Federation with AWS Single Sign-On<br>AWS Docs – AWS IAM Identity Center User Guide |
| 4 | - Study the module Encryption with AWS Key Management Service (KMS)<br>- Distinguish AWS managed keys from customer managed keys; learn envelope encryption and key rotation<br>- Learn how key policies work together with IAM policies<br>- Encrypt an S3 bucket or EBS volume with KMS and test the kms:Decrypt permission | 15/10/2026 | 15/10/2026 | AWS Cloud Journey – Encryption with AWS Key Management Service (KMS)<br>AWS Docs – AWS KMS Developer Guide |
| 5 | - Study the module Credentials Management with AWS Secrets Manager<br>- Store database connection details as a secret and retrieve them with the CLI/SDK<br>- Learn automatic rotation<br>- Compare with Systems Manager Parameter Store and note per-secret pricing | 16/10/2026 | 16/10/2026 | AWS Cloud Journey – Credentials Management with AWS Secrets Manager<br>AWS Docs – AWS Secrets Manager User Guide |

### Week 5 Achievements:

- Understood why an Allow can still be denied (explicit deny, boundaries, key policies) and how to check with the Policy Simulator.
- Understood how a permission boundary caps permissions during delegation.
- Used SSO for temporary-credential access instead of long-term access keys.
- Understood that KMS encryption does not replace access control: anyone allowed to decrypt can still read the data.
- Learned to store secrets in Secrets Manager instead of hard-coding them in source code.