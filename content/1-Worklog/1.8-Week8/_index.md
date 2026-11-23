---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

- Automate operations with Lambda using least-privilege execution roles.
- Manage infrastructure as code with CloudFormation and CDK.
- Learn system patching with EC2 Image Builder.
- Understand highly available web architectures.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study the module Serverless Automation with AWS Lambda<br>- Create the first Lambda function with an execution role holding only the necessary permissions<br>- Configure a trigger (EventBridge or S3) and view logs in CloudWatch<br>- Learn the risk of attaching an overly broad role to Lambda | 02/11/2026 | 02/11/2026 | AWS Cloud Journey – Serverless Automation with AWS Lambda<br>AWS Docs – AWS Lambda Developer Guide |
| 2 | - Study the module Infrastructure as Code with AWS CloudFormation<br>- Write a template creating a VPC, Security Group, or EC2 and deploy it as a stack<br>- Learn parameters, change sets, and drift detection<br>- Clean up by deleting the stack | 03/11/2026 | 03/11/2026 | AWS Cloud Journey – Infrastructure as Code with AWS CloudFormation<br>AWS Docs – AWS CloudFormation User Guide |
| 3 | - Study the module Cloud Development Kit (AWS CDK) Essentials<br>- Initialize a CDK project and learn constructs, stacks, synth, and deploy<br>- Compare CDK with CloudFormation<br>- Note the benefits of infrastructure as code: repeatable, reviewable, fewer misconfigurations | 04/11/2026 | 04/11/2026 | AWS Cloud Journey – Cloud Development Kit (AWS CDK) Essentials<br>AWS Docs – AWS CDK Developer Guide |
| 4 | - Study the module Systems Patching with EC2 Image Builder<br>- Create an image pipeline and recipe to build a standard AMI<br>- Relate it to Systems Manager Patch Manager and the customer's responsibility for patching the OS on EC2<br>- Record a routine for refreshing AMIs | 05/11/2026 | 05/11/2026 | AWS Cloud Journey – Systems Patching with EC2 Image Builder<br>AWS Docs – EC2 Image Builder User Guide |
| 5 | - Study the modules Scaling Applications with EC2 Auto Scaling and Building Highly Available Web Applications<br>- Design an architecture with ALB + Auto Scaling + Multi-AZ + RDS Multi-AZ<br>- Define Security Groups for each tier (ALB, application, database)<br>- Delete resources after practice | 06/11/2026 | 06/11/2026 | AWS Cloud Journey – Scaling Applications with EC2 Auto Scaling<br>AWS Cloud Journey – Building Highly Available Web Applications<br>AWS Docs – Amazon EC2 Auto Scaling User Guide |

### Week 8 Achievements:

- Granted minimal permissions to Lambda and understood the risk of overly broad roles.
- Deployed infrastructure with CloudFormation/CDK and understood the benefits of consistency and reviewability.
- Understood the role of standard AMIs and routine patching for EC2 workloads.
- Designed a highly available web architecture with sensible Security Group layering.