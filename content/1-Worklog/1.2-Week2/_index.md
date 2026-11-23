---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

- Understand the IAM model (users, groups, roles, policies) and the least-privilege principle.
- Protect the account with MFA and avoid using the root user for daily work.
- Learn VPC networking basics: subnets, route tables, Internet Gateway, NAT Gateway, Security Groups, NACLs.
- Launch EC2 securely and use IAM roles instead of long-term access keys.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study the module Access Management with AWS IAM<br>- Distinguish root user, IAM users, groups, roles, and policies<br>- Learn the JSON policy structure (Effect, Action, Resource, Condition) and the least-privilege principle<br>- Read the Shared Responsibility Model and IAM security best practices | 21/09/2026 | 21/09/2026 | AWS Cloud Journey – Access Management with AWS IAM<br>AWS Docs – Security best practices in IAM (<https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html>)<br>AWS – Shared Responsibility Model (<https://aws.amazon.com/compliance/shared-responsibility-model/>) |
| 2 | - Enable MFA for the root user and create an admin IAM user to replace root for daily work<br>- Create a group, attach managed policies, and write a customer managed policy scoped to specific resources<br>- Use the IAM Policy Simulator to verify effective permissions<br>- Record results and the AccessDenied errors encountered | 22/09/2026 | 22/09/2026 | AWS Cloud Journey – Access Management with AWS IAM<br>AWS Docs – IAM Policy Simulator |
| 3 | - Study the module Networking Essentials with Amazon VPC<br>- Learn public/private subnets, route tables, Internet Gateway, and NAT Gateway<br>- Compare Security Groups (stateful) with Network ACLs (stateless)<br>- Create a VPC with a public and a private subnet and check the route tables | 23/09/2026 | 23/09/2026 | AWS Cloud Journey – Networking Essentials with Amazon VPC<br>AWS Docs – Amazon VPC User Guide |
| 4 | - Study the module Compute Essentials with Amazon EC2<br>- Launch an EC2 instance in a public subnet with a key pair and a Security Group allowing SSH only from my IP<br>- Connect over SSH and verify the configuration<br>- Learn instance types, EBS, and pricing; stop/terminate resources after practice | 24/09/2026 | 24/09/2026 | AWS Cloud Journey – Compute Essentials with Amazon EC2<br>AWS Docs – Amazon EC2 User Guide |
| 5 | - Study the module Instance Profiling with IAM Roles for EC2<br>- Create an IAM role and instance profile with S3 read access and attach it to EC2<br>- Access S3 from EC2 with the AWS CLI without any access key<br>- Learn about temporary credentials and the instance metadata service (IMDS) | 25/09/2026 | 25/09/2026 | AWS Cloud Journey – Instance Profiling with IAM Roles for EC2<br>AWS Docs – IAM roles for Amazon EC2 |

### Week 2 Achievements:

- Understood how IAM controls who can do what on which resources, and why the root user should only be used when strictly necessary.
- Practiced enabling MFA, creating an admin IAM user, writing scoped policies, and testing them with the Policy Simulator.
- Understood the basic VPC structure and the difference between Security Groups and Network ACLs.
- Launched EC2 with SSH restricted by Security Group and cleaned up resources afterwards.
- Understood why IAM roles (temporary credentials) are preferred over long-term access keys.