---
title: "Event 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Summary Report: “First Cloud AI Journey: Weekly Meet Up”

- **Event Name:** First Cloud AI Journey: Weekly Meet Up  
- **Date & Time:** 09:00 – 12:00, October 24, 2026  
- **Location:** 26th Floor Bitexco Financial Tower, 2 Hai Trieu Street, Saigon, Ho Chi Minh City 700000, Vietnam 
- **Role:** Attendee  

### Event Objectives

- Learn practical engineering experience on Cloud and AI Agents directly from Tech Leads and industry engineers
- Explore real-world patterns across low-latency Vietnamese Voice AI, multi-account resource sharing, early infrastructure security testing, and production AI agent platforms
- Connect takeaways on cost optimization, context/memory management, security guardrails, and 24/7 agent operations with my learning path
- Build greater confidence in networking, proactive connection, and continuous learning within the community

### Speakers

- **Kiet Tran** – Revve AI
- **Long Huynh** – Styl Solution
- **Thinh Nguyen** – Styl Solution
- **Xuan An** – Leader of AWS Student Builder Group HCMUTE
- **Khoa Kieu** – Tech Lead at ACB
- **Nghi Danh** – AWS Community Builder

### Key Highlights

#### 1. Hear, Think, Speak – Building a Vietnamese Voice-AI Contact Center on AWS (Kiet Tran, Revve AI)

- Explored a **Voice AI** architecture focused on reducing response latency to around **1.8 seconds** for natural conversation
- Featured a live demo where the AI called a candidate directly to conduct a preliminary **Cloud Engineer** interview in Vietnamese

#### 2. AWS Resource Access Manager (Long Huynh, Styl Solution)

- Shared how to share resources safely across accounts within an **AWS Organization** to save costs and centralize network management
- Highlighted tightly combining **IAM policies** with **Service Control Policies (SCPs)** so no account or user exceeds its permission ceiling

#### 3. AWS Pentest with AWS Continuum / Security Agent (Thinh Nguyen, Styl Solution)

- Introduced an early infrastructure security assessment workflow by reviewing **Terraform** code and integrating checks into **GitLab/GitHub** pull requests to catch issues early
- Demonstrated having a **Security Agent** act like a real user to run automated penetration tests on **SIT/UAT** environments before production deployment

#### 4. Amazon Bedrock AgentCore (Xuan An, Leader of AWS Student Builder Group HCMUTE)

- Provided a comprehensive view of two platforms for taking AI agents into production:
  - **Agent Runtime**: Runs **MicroVMs** on **EC2 Spot** instances for cost-efficient execution
  - **Memory System**: Uses a synchronous **Short-term** tier and an asynchronous **Long-term** tier so the agent understands user context deeply

#### 5. Kiro Crew (Khoa Kieu, Tech Lead at ACB; Nghi Danh, AWS Community Builder)

- My favorite session, focusing on running AI agents **24/7** to support code review and system checks, with an engaging technical Q&A covering:
  - **Artifacts**: Automatically scraping real job data and generating visual statistical charts directly inside the chat window
  - **Context Window Management**: **Auto Compact** when context reaches **70–90%**, and **“Break down context”** to inspect token consumption per component in detail
  - **Memory & Guardrails**: Cleaning up old memory to prevent cost bloat, while enforcing a security guardrail layer to stop the AI from autonomously deleting infrastructure or leaking server secrets and credentials

### Key Takeaways

#### Multi-Account Governance & Shift-Left Security

- **Permission ceilings in shared AWS environments**: Combining **IAM policies** and **SCPs** alongside cross-account resource sharing helps optimize cost and centralize networking while keeping strict permission boundaries
- **Catching issues before production**: Reviewing **Terraform** in pull requests and running automated **Security Agent** pentests on **SIT/UAT** shifts security checks earlier before real deployment

#### Production AI Agents, Cost & Guardrails

- **Runtime and tiered memory**: Production agents rely on cost-conscious execution (**MicroVMs** on **EC2 Spot**) and layered short-term (synchronous) and long-term (asynchronous) memory for deeper context
- **Controlling cost and preventing risky actions**: Managing context windows (**Auto Compact**, **Break down context**), cleaning up stale memory, and applying guardrails keep 24/7 agents cost-effective and prevent unauthorized infrastructure deletion or secret/credential leaks

### Applying to Work

- **Pair IAM policies with SCPs**: Apply permission ceilings when sharing resources across accounts in an **AWS Organization**
- **Embed early security checks**: Review **Terraform** changes in pull requests and automate **SIT/UAT** security testing before production release
- **Manage context, memory, and guardrails in agents**: Monitor token usage with context breakdown/compaction, clean up old memory, and enforce guardrails that protect infrastructure, secrets, and credentials
- **Grow through proactive networking and study**: Push myself to be more confident in networking, proactive in connecting with speakers and peers, and more disciplined in studying

### Event Experience

Attending the **“First Cloud AI Journey: Weekly Meet Up”** on Saturday morning at Bitexco was a memorable experience that showed how broad and engaging real-world engineering is when Tech Leads and practitioners share hands-on lessons on Cloud and AI Agents. Key experiences included:

#### Learning from experienced practitioners
- Hearing from speakers across **Revve AI**, **Styl Solution**, **AWS Student Builder Group HCMUTE**, **ACB**, and the **AWS Community Builder** program made real-world architectures and trade-offs come alive.
- **Kiro Crew** stood out as my favorite session, especially the deep technical Q&A on **Artifacts**, **Auto Compact**, **Break down context**, memory cleanup, and guardrails for **24/7** agents.

#### Technical exposure
- Gained practical exposure to low-latency **Voice AI** (~1.8s response with a live Vietnamese Cloud Engineer interview demo), **AWS Resource Access Manager** with **IAM** and **SCPs**, **Terraform** PR reviews and **SIT/UAT** **Security Agent** pentesting, and **Amazon Bedrock AgentCore** (**Agent Runtime** on **EC2 Spot** MicroVMs and short/long-term **Memory**).

#### Networking and community spirit
- Being in the same room at Bitexco with speakers, organizers, and fellow learners created an inspiring environment that motivated my cloud journey.
- The meet-up reminded me to step out of my comfort zone, network with more confidence, and reach out more proactively.

#### Lessons learned
- Real-world Cloud and AI Agent engineering balances capability with latency, cost control, and strong guardrails.
- Operating AI agents continuously requires active context/memory hygiene and strict security guardrails so automation never deletes infrastructure or exposes secrets and credentials.
- Confidence in networking, proactive connection, and consistent learning effort are essential to keeping momentum in my cloud journey.

#### Some event photos
*Add your event photos here*  

> Overall, the meet-up packed a great deal of practical insight into a single morning—from Voice AI and multi-account governance to early security testing and 24/7 agent guardrails—while motivating me to network and learn more proactively.