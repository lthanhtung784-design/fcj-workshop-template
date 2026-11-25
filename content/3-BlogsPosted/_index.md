---
title: "Blogs Posted"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---



This section lists and introduces the blogs posted to [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj), focusing on AWS security mechanics, least privilege, data protection, and incident response.

### [Blog 1 - DOES SQS FIFO REALLY GUARANTEE “EXACTLY-ONCE PROCESSING”?](3.1-Blog1/)
This blog clarifies why duplicate processing can still happen on Amazon SQS FIFO queues—such as when a Lambda function writes to DynamoDB and times out before deleting the message—by distinguishing queue-level deduplication (5-minute window, SHA-256 on message body only) from end-to-end business effects, while covering Lambda at-least-once retries, idempotency (`ConditionExpression` on `PutItem`), external side effects, `ReportBatchItemFailures` on FIFO queues, FIFO DLQ redrive trade-offs, and four core async design questions.

### [Blog 2 - AWS KMS & ENVELOPE ENCRYPTION: IS DATA ENCRYPTION ALREADY SECURE ENOUGH?](3.2-Blog2/)
This blog examines how S3 SSE-KMS uses envelope encryption (`GenerateDataKey` and data keys vs. KMS keys), why encryption at rest does not replace authorization, how encryption context works as non-secret AAD, and how S3 Bucket Keys reduce KMS request costs (up to 99%) while shifting default `aws:s3:arn` from object ARN to bucket ARN and affecting KMS policy evaluation and CloudTrail granularity.

### [Blog 3 - HAS AMAZON S3 BLOCK PUBLIC ACCESS ALREADY MADE YOUR DATA SAFE?](3.3-Blog3/)
This blog explores why enabling S3 Block Public Access does not stop unauthorized reads with leaked valid credentials, structuring S3 protection across three layers: Prevention (four Block Public Access settings, least privilege, Bucket owner enforced, default SSE-S3), Auditing (CloudTrail S3 Data Events), and Detection & Alerting (GuardDuty S3 Protection via EventBridge and SNS).

### [Blog 4 - HOW CAN A SINGLE IAM PERMISSION CAUSE MAJOR RISKS? ANALYZING ADMINISTRATORACCESS ON AWS](3.4-Blog4/)
This blog analyzes the blast-radius risks of over-privileged IAM identities using `AdministratorAccess`—covering S3 data exposure/deletion, EC2 abuse such as cryptojacking, RDS disruption, IAM privilege escalation/persistence, and CloudTrail tampering—alongside controls like least privilege, MFA, temporary credentials via IAM roles, permission boundaries, CloudTrail monitoring, and regular access reviews.

### [Blog 5 - AWS ACCESS KEY EXPOSED ON GITHUB: AWS ALREADY QUARANTINED IT—WHAT ELSE MUST WE DO?](3.5-Blog5/)
This blog explains what AWS does automatically when an access key is exposed on GitHub (attaching quarantine policies such as `AWSCompromisedKeyQuarantineV3` or `AWSCompromisedKeyQuarantineV4` and notifying via AWS Health or Support Case), outlines the 5-step response workflow, and highlights preventive controls including IAM roles, IAM Identity Center, GitHub Actions OIDC, Secret Scanning with Push Protection, and `git-secrets`.