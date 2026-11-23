---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

- Design backup and recovery with AWS Backup and EBS Data Lifecycle Manager.
- Understand disaster recovery with Elastic Disaster Recovery.
- Learn the incident response process for a leaked access key.
- Learn application user authentication with Amazon Cognito.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study the module Data Protection with AWS Backup<br>- Create a backup plan, vault, and retention policy<br>- Practice backing up and test-restoring a resource<br>- Learn vault lock and copying to another account/region to resist ransomware | 26/10/2026 | 26/10/2026 | AWS Cloud Journey – Data Protection with AWS Backup<br>AWS Docs – AWS Backup Developer Guide |
| 2 | - Study the module Snapshot Automation with Amazon EBS Data Lifecycle Manager<br>- Create a lifecycle policy that takes scheduled snapshots and retains them by count<br>- Study the module Anomaly Detection for EBS Backups<br>- Record how to monitor backups to detect issues early | 27/10/2026 | 27/10/2026 | AWS Cloud Journey – Snapshot Automation with Amazon EBS Data Lifecycle Manager<br>AWS Cloud Journey – Anomaly Detection for EBS Backups<br>AWS Docs – Amazon Data Lifecycle Manager |
| 3 | - Study the module Disaster Recovery with AWS Elastic Disaster Recovery<br>- Distinguish RPO, RTO, and DR strategies<br>- Learn continuous replication, drills, and recovery<br>- Compare Elastic Disaster Recovery with regular backups | 28/10/2026 | 28/10/2026 | AWS Cloud Journey – Disaster Recovery with AWS Elastic Disaster Recovery<br>AWS Docs – AWS Elastic Disaster Recovery User Guide |
| 4 | - Research the process for handling an AWS access key leaked on GitHub<br>- Understand that AWS attaches a quarantine policy but does not disable the key<br>- Summarize the steps: set the key to Inactive, replace credentials, investigate with CloudTrail, review the account<br>- Write a study-group post to share the findings | 29/10/2026 | 29/10/2026 | AWS Security Blog – What to do if you inadvertently expose an AWS access key (<https://aws.amazon.com/blogs/security/what-to-do-if-you-inadvertently-expose-an-aws-access-key>)<br>AWS re:Post – How AWS responds to exposed credentials (<https://repost.aws/articles/ARoBXj63rWSt2Ww7XKlVV72g/how-aws-responds-to-exposed-credentials-and-how-you-can-protect-your-account>)<br>Unit 42 – Detecting exposed AWS IAM credentials (<https://unit42.paloaltonetworks.com/detecting-exposed-aws-iam-credentials/>)<br>GitHub Docs – Secret scanning and push protection (<https://docs.github.com/en/code-security/secret-scanning/working-with-secret-scanning-and-push-protection>)<br>AWS Labs – git-secrets (<https://github.com/awslabs/git-secrets>) |
| 5 | - Study the module Cross-Domain Authentication with Amazon Cognito<br>- Distinguish user pools from identity pools<br>- Learn OAuth 2.0/OIDC, the hosted UI, and MFA for application users<br>- Record common configuration mistakes | 30/10/2026 | 30/10/2026 | AWS Cloud Journey – Cross-Domain Authentication with Amazon Cognito<br>AWS Docs – Amazon Cognito Developer Guide |

### Week 7 Achievements:

- Understood that backups are useful only with retention policies, protection against accidental deletion, and regular restore tests.
- Distinguished backup from disaster recovery and learned RPO/RTO.
- Learned the incident response process for a leaked access key and completed a sharing post.
- Understood how Cognito authenticates application users and how it differs from IAM.