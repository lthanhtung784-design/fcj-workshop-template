---
title: "5.3 · Deploy the application"
weight: 3
chapter: false
---

Start with the backend. The portal needs its stack outputs, and the web ACL needs the portal distribution ID.

| Section | Outcome |
|---|---|
| [5.3.1 · Backend and image processing](backend/) | Create the main SAM stack and verify the two extraction layers. |
| [5.3.2 · Portal and access control](portal/) | Configure Cognito, CloudFront origins and the live frontend. |
| [5.3.3 · Protect CloudFront with WAF](waf/) | Associate the ACL, prove the header block and run the portal regression. |
