---
title: "5.2 · Prerequisites"
weight: 2
chapter: false
aliases:
  - /5-workshop/02-prerequisites/
---

Use a dedicated lab account in **us-east-1**. Some physical names are fixed. On an existing deployment, go to the audit chapter before creating anything. Install Git, x64 Python 3.12, Node.js 22, AWS CLI v2 and AWS SAM CLI. Docker is optional for Linux container builds. Arrange stack deployment and pass-role permissions with the account owner. Use a domain/subdomain you can configure and distinct controlled email addresses for Reporter, a second Reporter, Admin and Auditor.

Extract [PhishGuard-Lab.zip](/downloads/PhishGuard-Lab.zip) and start PowerShell in the directory containing `lab` and `tools`. Configure the deployment profile `phishguard`. Only the application users sign in to Cognito. Keep the same shell for the following chapters.

```powershell
Set-Location .\lab
$pgProfile = 'phishguard'
$pgRegion = 'us-east-1'
$pgStack = 'phishguard-ai'
aws sts get-caller-identity --profile $pgProfile --query '{Account:Account,Arn:Arn}'
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements-dev.txt
.\.venv\Scripts\python.exe -m pip install "moto[s3,dynamodb]==5.2.5"
sam --version
node --version
Test-Path .\layers\ocr-vie-py312-x86_64.zip
```

Check the account ARN, SAM version and that the OCR layer check returns `True`. For an expired SSO session use `aws sso login --profile phishguard`.

In the same shell check the second image layer and the playbooks supplied with the full lab. Expect True and five files. If your AWS profile is named differently, set $pgProfile to that existing profile for the following commands.

```powershell
Test-Path .\layers\qr-py312-x86_64.zip
(Get-ChildItem .\kb-docs\playbooks\*.txt).Count
```

