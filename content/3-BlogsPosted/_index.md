---
title: "Blogs Posted"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}

This section lists and introduces the blogs posted to [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj), focusing on AWS security mechanics, least privilege, data protection, and incident response.

### [Blog 1 - ...](3.1-Blog1/)
Add a brief summary for Blog 1 here once its source post is finalized in the series.

### [Blog 2 - AWS KMS & ENVELOPE ENCRYPTION: IS DATA ENCRYPTION ALREADY SECURE ENOUGH?](3.2-Blog2/)
This blog examines how S3 SSE-KMS uses envelope encryption (`GenerateDataKey` and data keys vs. KMS keys), why encryption at rest does not replace authorization, how encryption context works as non-secret AAD, and how S3 Bucket Keys reduce KMS request costs (up to 99%) while shifting default `aws:s3:arn` from object ARN to bucket ARN and affecting KMS policy evaluation and CloudTrail granularity.

### [Blog 3 - HAS AMAZON S3 BLOCK PUBLIC ACCESS ALREADY MADE YOUR DATA SAFE?](3.3-Blog3/)
This blog explores why enabling S3 Block Public Access does not stop unauthorized reads with leaked valid credentials, structuring S3 protection across three layers: Prevention (four Block Public Access settings, least privilege, Bucket owner enforced, default SSE-S3), Auditing (CloudTrail S3 Data Events), and Detection & Alerting (GuardDuty S3 Protection via EventBridge and SNS).

### [Blog 4 - HOW CAN A SINGLE IAM PERMISSION CAUSE MAJOR RISKS? ANALYZING ADMINISTRATORACCESS ON AWS](3.4-Blog4/)
This blog analyzes the blast-radius risks of over-privileged IAM identities using `AdministratorAccess`—covering S3 data exposure/deletion, EC2 abuse such as cryptojacking, RDS disruption, IAM privilege escalation/persistence, and CloudTrail tampering—alongside controls like least privilege, MFA, temporary credentials via IAM roles, permission boundaries, CloudTrail monitoring, and regular access reviews.

### [Blog 5 - AWS ACCESS KEY EXPOSED ON GITHUB: AWS ALREADY QUARANTINED IT—WHAT ELSE MUST WE DO?](3.5-Blog5/)
This blog explains what AWS does automatically when an access key is exposed on GitHub (attaching quarantine policies such as `AWSCompromisedKeyQuarantineV3` or `AWSCompromisedKeyQuarantineV4` and notifying via AWS Health or Support Case), outlines the 5-step response workflow, and highlights preventive controls including IAM roles, IAM Identity Center, GitHub Actions OIDC, Secret Scanning with Push Protection, and `git-secrets`.