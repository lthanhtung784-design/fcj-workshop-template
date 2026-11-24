---
title: "Event 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Summary Report: “AWS Cloud & AI Day Hanoi 2026”

- **Event Name:** AWS Cloud & AI Day Hanoi 2026
- **Date & Time:** 09:00-17:00, September 29, 2026 
- **Location:** 26th Floor Bitexco Financial Tower, 2 Hai Trieu Street, Saigon, Ho Chi Minh City 700000, Vietnam
- **Role:** Attendee

### Event Objectives

- Understand how cloud, generative AI, and agentic AI are evolving from experimental technologies into production-grade enterprise capabilities
- Explore modern approaches to cloud-native application development, infrastructure, data platforms, workload identity, security, and AI governance
- Learn from real-world AWS customer cases how organizations in Vietnam are modernizing their systems and operating them at enterprise scale
- Understand how security, governance, observability, and human oversight must evolve as AI systems become increasingly autonomous
- Connect the topics presented at the event with my own learning path in cybersecurity and cloud security

### Speakers

- **Dr. Werner Vogels** – CTO, Amazon.com (keynote speaker)
- **Eric Yeo** – Country General Manager for Malaysia, Vietnam & Indochina, AWS
- **Mai Le** – Director of Product Management, Katalon
- **Dr. Jens Lottner** – Chief Executive Officer, Techcombank
- **AWS experts, engineers, architects, and technology leaders** from Katalon, Techcombank, TCBS, Techcom Life, VPBank, and other organizations

### Key Highlights

#### From Cloud-Native Architecture to Agentic AI

- Shift from simply migrating workloads to the cloud toward building cloud-native, automated, and increasingly autonomous systems using **containers**, **Kubernetes**, **serverless**, **event-driven architectures**, and **managed cloud services**
- **Platform Engineering** and **Internal Developer Platforms (IDPs)** create standardized **“Golden Paths”** to reduce manual infrastructure work and **TicketOps** bottlenecks
- Technologies such as **Amazon EKS**, **Crossplane**, **Terragrunt**, **Backstage**, **FluxCD**, and **GitOps** enable reproducible, automated, consistent, traceable, and controlled infrastructure and application delivery

#### Agentic AI: From Proof of Concept to Production

- Building an AI agent is easier than operating one safely in production, requiring four key pillars:
  - **Operational excellence**: Reliability, failure handling, latency, and operational monitoring
  - **Data governance**: Data ownership, freshness, quality, and access authorization
  - **Security and trust**: Controlling identities, tools, permissions, and sensitive information
  - **Human oversight**: Maintaining human responsibility for high-impact or irreversible actions
- Sessions covering **Amazon Bedrock**, **Amazon Bedrock AgentCore**, **Strands Agents**, **Model Context Protocol (MCP)**, the **ReAct** pattern, state management, and tool integration showed how agents reason, retrieve information, call tools, maintain context, and act safely within clear authorization boundaries

#### Identity, Least Privilege, and AI Security

- Moving beyond removing long-lived access keys to verifiable **workload identity** across trust boundaries
- Key mechanisms: **AWS IAM**, **AWS STS** (short-lived credentials and sessions), **trust policies**, **session policies and session tags**, **source identity**, and **ABAC** across **EC2**, **ECS/Fargate**, **Lambda**, **EKS**, **CI/CD**, cross-account workloads, and **AI agents**

#### AI Governance, Data Security, and Trust

- Enterprise AI is a data and governance problem as much as a model problem, covering data accuracy, freshness, origin, ownership, access authorization, evidence-backed answers, traceability, and handling unsafe agent decisions
- Focused on data lineage, freshness, quality, permissions, and provenance, summarized along the security chain: **Identity → Data → Model → Tools → Agent → Action → Audit**

#### Security Observability for AI Applications

- Extends traditional monitoring (**Four Golden Signals**: Latency, Errors, Traffic, Saturation) with AI dimensions:
  - **Cost**: Token consumption and unexpected usage
  - **Safety**: PII exposure, prompt injection, and unsafe tool execution
  - **Quality**: Hallucinations and incorrect outputs
- Combines infrastructure telemetry, security events, data access, and AI-agent behavior

#### Secure AI-Assisted Software Development

- **Kiro** and **AI-DLC** extend AI across the SDLC (planning and design, code generation and testing, documentation and deployment, technical-debt management, migration and modernization), with the **TCBS** case reporting a **26%** reduction in development time
- Requires validation, security review, governance, human approval, and **DevSecOps** integration

#### Cloud Modernization and Enterprise Security

- Customer cases from **Techcombank**, **Techcom Life**, **TCBS**, **VPBank**, and **Katalon** highlighted application/database modernization, containerization, data-platform consolidation, infrastructure automation, observability, security, compliance, data residency, and operational resilience
- Covered **AWS Local Zone in Hanoi** and **AWS Outposts (second generation)** for data-residency and regulatory requirements, balancing **Security + Compliance + Reliability + Performance + Cost + Business Agility**

### Key Takeaways

#### Security Mindset

- **Identity as a security boundary**: Every workload, pipeline, service, and AI agent needs a clearly defined identity with short-lived, least-privilege credentials
- **Full-chain AI security and human oversight**: Protect the entire chain (**Identity → Data → Model → Tools → Agent → Action → Audit**) and keep human oversight for high-risk or irreversible actions
- **Broader AI observability**: Monitor behavior, data access, AI safety, quality, and cost alongside traditional metrics

#### Cloud & Technical Architecture

- **Reproducible, traceable infrastructure**: Favor managed services, containers, Kubernetes, serverless, automation, **GitOps**, and **IDPs** over manual SSH changes
- **Strong identity and data foundations**: Combine **IAM**, **STS**, workload identity, **ABAC**, cross-account access, trusted data, and governance

#### AI & Cybersecurity

- **Safe execution over capability alone**: Verify whether an agent acts safely with the right identity, permissions, data, and evidence against new attack surfaces (prompt injection, data exposure, excessive permissions, unauthorized actions, hallucinations, uncontrolled costs)
- **Intersection of disciplines**: Connects **Cloud Security**, **DevSecOps**, **AI Security**, and **Security Operations**

### Applying to Work

- **Apply least-privilege IAM and short-lived credentials**: Practice **AWS IAM**, **STS**, role assumption, trust policies, **ABAC**, and cross-account access (such as a lab with a role, trust policy, and session tags reviewed in audit logs)
- **Expand security monitoring**: Combine infrastructure logs, identity events, application telemetry, and AI-agent activity, and explore extending **Wazuh** and **SIEM** concepts toward cloud and AI security
- **Adopt GitOps, IaC, and AI agent boundaries**: Keep infrastructure changes traceable and auditable, and define explicit identity, permission, data-access, logging, and human-approval boundaries when experimenting with AI agents
- **Maintain human review with AI dev tools**: Use AI development tools to boost productivity while keeping security validation and human approval, bridging network/endpoint security with cloud-native security

### Event Experience

Attending the **“AWS Cloud & AI Day Hanoi 2026”** workshop was extremely valuable, giving me a comprehensive view of how cloud-native architectures, agentic AI, and enterprise security operate at scale. Key experiences included:

#### Learning from industry experts
- Talks from AWS leaders and enterprise customers (**Techcombank**, **TCBS**, **VPBank**, **Techcom Life**, and **Katalon**) showed how companies modernize systems and balance technology with governance, operations, security, and organizational change.
- Real-world enterprise cases grounded abstract cloud and AI concepts in production scale and regulatory realities.

#### Technical exposure
- Gained conceptual exposure to **Amazon EKS**, **Kubernetes**, **GitOps**, **IAM**, **STS**, **Bedrock**, **AgentCore**, **MCP**, **AI-DLC**, data governance, and **AI observability**.
- Deepened my understanding of workload identity, least privilege, infrastructure automation, and monitoring AI safety, quality, and cost.

#### Lessons learned
- Automation without governance can raise risk as fast as it raises productivity.
- The more autonomous a system is, the stricter its identity and authorization controls need to be, built on trusted data and integrated security across the lifecycle and AI governance.
- Security practitioners need to understand how to secure, monitor, and govern AI systems as well as detect attacks.

#### Some event photos
*Add your event photos here*

> Overall, the event not only provided broad technical and security insights, but also helped shape my approach to cloud security, governance, observability, and safe AI adoption.
```[cite: 5]