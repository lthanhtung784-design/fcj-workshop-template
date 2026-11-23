---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

- Understand private access to S3 through VPC endpoints.
- Monitor network traffic with VPC Flow Logs.
- Administer EC2 without opening SSH ports using Systems Manager Session Manager.
- Organize resources with tags and control permissions by tag.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study the module Private Access to S3 with VPC Endpoints<br>- Learn gateway endpoints and how route tables are updated<br>- Configure an endpoint policy to limit which buckets can be accessed<br>- Verify that EC2 in a private subnet reaches S3 without traversing the Internet | 05/10/2026 | 05/10/2026 | AWS Cloud Journey – Private Access to S3 with VPC Endpoints<br>AWS Docs – Gateway endpoints for Amazon S3 |
| 2 | - Study the module Network Monitoring with VPC Flow Logs<br>- Enable Flow Logs and deliver them to CloudWatch Logs or S3<br>- Read ACCEPT/REJECT records and recognize automated port-scanning traffic<br>- Relate the findings to tightening Security Groups and Network ACLs | 06/10/2026 | 06/10/2026 | AWS Cloud Journey – Network Monitoring with VPC Flow Logs<br>AWS Docs – Logging IP traffic using VPC Flow Logs |
| 3 | - Study the module Systems Management with AWS Systems Manager<br>- Learn the main features (Run Command, Patch Manager, Parameter Store)<br>- Attach the AmazonSSMManagedInstanceCore role to EC2 so Systems Manager can manage it<br>- Record the conditions for an instance to appear in Fleet Manager | 07/10/2026 | 07/10/2026 | AWS Cloud Journey – Systems Management with AWS Systems Manager<br>AWS Docs – AWS Systems Manager User Guide |
| 4 | - Study the module Remote Server Access with Systems Manager Session Manager<br>- Connect to EC2 without opening port 22 or using a key pair<br>- Learn how access is controlled with IAM and how sessions can be logged<br>- Compare Session Manager with traditional SSH | 08/10/2026 | 08/10/2026 | AWS Cloud Journey – Remote Server Access with Systems Manager Session Manager<br>AWS Docs – AWS Systems Manager Session Manager |
| 5 | - Study the module Resource Organization with Tags and Resource Groups<br>- Design a tagging convention (Project, Owner, Environment) and group resources with Resource Groups<br>- Study the module Access Control with IAM and Resource Tags<br>- Practice policies with tag-based conditions (attribute-based access control) | 09/10/2026 | 09/10/2026 | AWS Cloud Journey – Resource Organization with Tags and Resource Groups<br>AWS Cloud Journey – Access Control with IAM and Resource Tags<br>AWS Docs – Tagging AWS resources<br>AWS Docs – Controlling access to AWS resources using tags |

### Week 4 Achievements:

- Understood how EC2 in a private subnet can reach S3 through a gateway endpoint restricted by an endpoint policy.
- Read Flow Logs to recognize rejected traffic and unusual connections.
- Managed EC2 through Session Manager without opening SSH ports.
- Designed a tagging convention and used tags for access control.
- Understood the link between network monitoring, reducing the attack surface, and centralized management.