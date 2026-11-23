---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

- Host a static website on S3 and understand key S3 security settings.
- Use the AWS CLI with profiles for safe and repeatable operations.
- Set up basic monitoring and alerting with CloudWatch.
- Understand how to deploy RDS in a private subnet.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study the module Static Website Hosting with Amazon S3<br>- Create a bucket, enable static website hosting, and upload index.html<br>- Configure a bucket policy that allows public read only where needed<br>- Learn common 403 errors when hosting static websites | 28/09/2026 | 28/09/2026 | AWS Cloud Journey – Static Website Hosting with Amazon S3<br>AWS Docs – Hosting a static website using Amazon S3 |
| 2 | - Study the module S3 Security Best Practices<br>- Learn the 4 S3 Block Public Access options and how AWS applies the most restrictive combination<br>- Distinguish bucket policies, ACLs, and Object Ownership (bucket owner enforced)<br>- Learn default SSE-S3 encryption, versioning, and access logging (CloudTrail data events)<br>- Verify settings with aws s3api get-public-access-block | 29/09/2026 | 29/09/2026 | AWS Cloud Journey – S3 Security Best Practices<br>AWS Docs – Security best practices for Amazon S3<br>AWS Docs – Blocking public access to your Amazon S3 storage |
| 3 | - Study the module Command Line Operations with AWS CLI<br>- Install the AWS CLI and configure profiles (aws configure / SSO)<br>- Practice commands for S3, EC2, and IAM using --query and --output<br>- Learn how to store credentials safely on a personal machine and keep them out of repositories | 30/09/2026 | 30/09/2026 | AWS Cloud Journey – Command Line Operations with AWS CLI<br>AWS Docs – AWS CLI User Guide |
| 4 | - Study the module Monitoring with Amazon CloudWatch<br>- View EC2 metrics and learn CloudWatch Logs and dashboards<br>- Create a CPU alarm that sends notifications through Amazon SNS (email)<br>- Confirm the SNS subscription and verify that the alarm works | 01/10/2026 | 01/10/2026 | AWS Cloud Journey – Monitoring with Amazon CloudWatch<br>AWS Docs – Amazon CloudWatch User Guide |
| 5 | - Study the module Database Essentials with Amazon RDS<br>- Learn Multi-AZ, automated backups, and DB subnet groups<br>- Create RDS in a private subnet with a Security Group allowing access only from the application server<br>- Learn encryption at rest and delete resources after practice to avoid charges | 02/10/2026 | 02/10/2026 | AWS Cloud Journey – Database Essentials with Amazon RDS<br>AWS Docs – Amazon RDS User Guide |

### Week 3 Achievements:

- Hosted a static website on S3 and understood that a private bucket does not mean every access is blocked.
- Learned the S3 protection layers: Block Public Access, bucket policies, encryption, versioning, and logging.
- Used the basic AWS CLI with profiles and learned how to avoid exposing credentials.
- Created a CloudWatch alarm with an SNS notification.
- Understood the pattern of placing databases in private subnets and controlling access with Security Groups.