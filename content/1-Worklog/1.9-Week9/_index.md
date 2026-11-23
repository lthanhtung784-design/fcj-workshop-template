---
title: "Week 9 Worklog"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

- Understand basic security practices with Docker and Amazon ECS.
- Build a CI/CD pipeline with CodePipeline without storing keys in the repository.
- Understand asynchronous messaging with SQS and SNS.
- Monitor serverless applications with X-Ray and CloudWatch.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study the module Containerization with Docker<br>- Write a Dockerfile, build and run a container<br>- Learn safe practices: small images, no root user, no secrets baked into images<br>- Learn image vulnerability scanning | 09/11/2026 | 09/11/2026 | AWS Cloud Journey – Containerization with Docker<br>Docker Docs – Dockerfile best practices |
| 2 | - Study the module Container Orchestration with Amazon ECS<br>- Create a cluster, task definition, and service with Fargate<br>- Distinguish the task role from the task execution role<br>- Inject secrets from Secrets Manager into the container instead of hard-coding environment variables | 10/11/2026 | 10/11/2026 | AWS Cloud Journey – Container Orchestration with Amazon ECS<br>AWS Docs – Amazon ECS Developer Guide |
| 3 | - Study the module CI/CD Pipeline with AWS CodePipeline<br>- Build a pipeline with source, build, and deploy stages<br>- Understand the pipeline's IAM service role and artifact store<br>- Confirm that no access keys are stored in source code or config files, linking back to the leaked-key lesson | 11/11/2026 | 11/11/2026 | AWS Cloud Journey – CI/CD Pipeline with AWS CodePipeline<br>AWS Docs – AWS CodePipeline User Guide<br>AWS Labs – git-secrets (<https://github.com/awslabs/git-secrets>) |
| 4 | - Study the module Messaging Systems with SQS and SNS<br>- Distinguish queues from topics and try publish/subscribe<br>- Configure a dead-letter queue and server-side encryption<br>- Learn queue/topic access policies to prevent unintended access | 12/11/2026 | 12/11/2026 | AWS Cloud Journey – Messaging Systems with SQS and SNS<br>AWS Docs – Amazon SQS Developer Guide<br>AWS Docs – Amazon SNS Developer Guide |
| 5 | - Study the module Distributed Tracing with X-Ray and CloudWatch<br>- Enable tracing for Lambda/API and read the service map<br>- Create CloudWatch alarms for errors and latency<br>- Summarize how to combine logs, metrics, and traces when investigating incidents | 13/11/2026 | 13/11/2026 | AWS Cloud Journey – Distributed Tracing with X-Ray and CloudWatch<br>AWS Docs – AWS X-Ray Developer Guide |

### Week 9 Achievements:

- Learned safe practices for packaging and running containers.
- Distinguished the task role from the execution role in ECS and retrieved secrets properly.
- Built a CI/CD pipeline without exposing credentials in the repository.
- Understood decoupling with SQS/SNS and protecting it with policies and encryption.
- Learned to combine logs, metrics, and traces for investigations.