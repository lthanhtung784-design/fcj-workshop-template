---
title: "Blog 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 3.5. </b> "
---


# AWS ACCESS KEY EXPOSED ON GITHUB: AWS ALREADY QUARANTINED IT—WHAT ELSE MUST WE DO?

When reading about exposed AWS access keys, it is easy to assume that automatic AWS detection and mitigation mean the risk is minor. In reality, AWS helps detect and limit impact, but automated quarantine does not mean the account is automatically safe or that incident response is finished. This post outlines what AWS does when an exposed key is detected, the five steps to respond, and ways to prevent exposure in personal and team projects.

Key points to remember:

- **What AWS Does Automatically:** AWS can detect credentials exposed on sources such as GitHub, attach quarantine policies (such as `AWSCompromisedKeyQuarantineV3` or `AWSCompromisedKeyQuarantineV4`) to the IAM identity, and notify via AWS Health or a Support Case (with Unit 42 observing a ~10-second V3 policy attachment in one test, though response time is not guaranteed). Quarantine policies add explicit `Deny` statements on specific actions rather than disabling the key outright, so remaining allowed actions still depend on the identity's other IAM permissions.
- **5-Step Incident Response:** (1) Isolate the exposed key by identifying the IAM user, checking permissions, and setting the key to `Inactive` first rather than deleting immediately when operational correlation helps; (2) restore legitimate access by updating workloads and migrating from long-term keys to IAM roles/temporary credentials; (3) investigate activity in AWS CloudTrail (APIs, timestamps, source IPs, regions, and IAM/resource changes) using an independent admin principal and accounting for log scope such as S3 data events; (4) check for compromise across the wider account (new/modified IAM users, roles, policies, EC2/Lambda/S3 resources, unusual regions, and billing anomalies); and (5) close out remediation by following the AWS Support Case guidance rather than removing the quarantine policy prematurely just because workloads recover.
- **Prevention First:** Favor IAM roles for AWS workloads, IAM Identity Center/federation over long-term user keys, GitHub Actions OIDC instead of long-lived secrets, GitHub Secret Scanning with Push Protection, and local hooks like `git-secrets`—and remember that deleting a file or commit does not make a leaked secret safe once exposed.
![Blog 5 screenshot](/images/3-BlogsPosted/3.5-Blog4/blog5.png)
https://www.facebook.com/groups/awsstudygroupfcj/permalink/2346834029414889/