---
title: "5.7 · COST · Estimate and billing"
weight: 7
chapter: false
aliases:
  - /5-workshop/08-cost/
---

PhishGuard has an estimated service cost of **USD 9.37 for 300 reports in a 30-day month**, before tax and domain renewal. The Cost Explorer export for **1–23 November 2026** rounds to **USD 0.00**. The estimate assumes a full month of WAF coverage. The documented WAF test took place on 23 November. One figure is a budget for continued operation. The other records what appeared in the account report during the lab period.

## 1. Scope and workload

The application runs in **US East (N. Virginia), `us-east-1`**, behind a **pay-as-you-go CloudFront** distribution protected by the `PhishGuardEdge` web ACL. Its final rule set includes one standard AWS managed rule group and one rate-based rule. The temporary header probe used for the 403 test is off. There are two observed alarms, covering workflow failures and the Ingest dead-letter queue. Viewing a WAF graph in the console adds no custom metric to this model.

The 300 reports include **90 images, 60 incoming SES messages and 90 cases reaching a decision**. These categories can overlap. The portal makes 12,000 HTTP API requests. CloudFront serves 20,000 HTTPS requests and 1 GB to viewers. For budgeting, every report makes one model call and one KB query. In practice some cases stop early for lack of evidence. A direct browser POST to S3 bypasses the CloudFront WAF request path.

## 2. Monthly estimate

| Cost item | Main input | USD/month |
|---|---|---:|
| AWS WAF | 1 ACL × USD 5 + 1 managed group × USD 1 + 1 rate rule × USD 1 + 0.02 million requests × USD 0.60 | 7.0120 |
| CloudFront | PAYG, 1 GB and 20,000 requests within the account’s remaining allowance | 0.0000 |
| AWS KMS | 1 customer-managed symmetric key, 2,400 requests | 1.0072 |
| Route 53 | One separately allocated public hosted zone and 1,000 standard DNS queries | 0.5004 |
| CloudWatch | Two standard alarms at one metric each, 0.1 GB of log ingestion and 0.05 GB-month stored | 0.2515 |
| Lambda and HTTP API | 13,380 x86 Lambda invocations, 1,860 GB-seconds and 12,000 HTTP API requests | 0.0457 |
| Step Functions Standard | 300 executions × 12 state transitions × USD 0.000025 | 0.0900 |
| Bedrock Nova Lite v1 | 0.6 million input tokens × USD 0.06 + 0.3 million output tokens × USD 0.24 | 0.1080 |
| Guardrails and Titan Text Embeddings V2 | 1,800 billable content-filter text units, 130,000 document and query embedding tokens | 0.2726 |
| S3 Standard and S3 Vectors | 1 GB-month, 1,500 writes, 6,000 reads. Vectors use 0.01 GB stored and written each, plus 300 small queries | 0.0363 |
| DynamoDB | On demand, 6,000 write and 30,000 read units, 0.05 GB-month each of storage and PITR | 0.0300 |
| SES, SNS and SQS | 60 messages and 60 billable inbound chunks, 90 publishes and 90 email deliveries, 1,000 SQS requests | 0.0136 |
| Cognito and Budgets | 10 direct sign-in users within the eligible allowance, one assumed notification-only cost budget | 0.0000 |
| **Total using unrounded line items** | **Before tax and domain renewal** | **9.37** |

The baseline uses the ACL/rule tariff for the November 2026 workshop. Check the **effective pricing period** in the Calculator. For usage starting on 1 February 2027, substitute **USD 7.212** for WAF at one distribution × 720 hours × USD 0.01 and the same request volume. That gives **USD 9.57**. Fixed fees on the ACL/rule tariff are prorated hourly, including the probe while it was present. [WAF rates and effective dates](https://aws.amazon.com/waf/pricing/)

Most lines use list rates. CloudFront and Cognito assume an eligible allowance is available. Credits, other free allowances, billing query fees and tax depend on the account. If DNS is shared and no DNS cost is allocated to the lab, the baseline is **USD 8.87**. One billable dashboard and one billable custom metric would add about **USD 3.30**, bringing the original full-zone scenario to **USD 12.67**. Add the registrar’s **actual annual renewal divided by 12** to budget for the domain. [CloudFront PAYG](https://aws.amazon.com/cloudfront/faqs/) · [CloudWatch](https://aws.amazon.com/cloudwatch/pricing/) · [Route 53](https://aws.amazon.com/route53/pricing/)

[Download the unit-by-unit estimate with rate sources (CSV)](/downloads/phishguard-cost-inputs.csv)

## 3. Reproduce the estimate in AWS Pricing Calculator

1. Open **AWS Pricing Calculator → Create estimate → Add service**. Name the group `PhishGuard | 300 reports`. Choose **US East (N. Virginia)** for regional services. For CloudFront select PAYG and the applicable viewer geography.
2. Enter WAF, KMS, CloudWatch and Route 53 first. For WAF enter **one** standard managed group and **one** rate rule. Leave the probe at zero. If a field takes millions of requests, enter **0.02** for 20,000. Use the table and CSV for the remaining services.
3. For Lambda choose **on-demand, x86**. Use the six lines below if the form accepts one memory/duration pair per entry. Extract includes Tesseract OCR and QR decoding. Step Functions holds the approval callback, so the 48-hour deadline adds no Lambda runtime while the workflow waits.
4. For Amazon Bedrock select **Amazon Nova Lite v1**, on demand. Enter **300** calls a month at **2,000 input and 1,000 output tokens** per call, or **600,000/300,000** monthly tokens where requested. For a feature the form does not cover, record the manual amount from the CSV. Add only items missing from the Calculator subtotal.
5. On **My Estimate**, use **Share/Save** and export the PDF. Place its link or the PDF beside the estimate. Record any free allowances or manual adjustments that explain a difference from USD 9.37. [AWS Pricing Calculator](https://calculator.aws/) · [Save and share an estimate](https://docs.aws.amazon.com/pricing-calculator/latest/userguide/save-share-estimate.html)

| Lambda line | Invocations/month | MiB | Assumed duration per invocation |
|---|---:|---:|---:|
| Reporter API + Admin API | 12,000 | 256 | 200 ms |
| Ingest + Triage | 600 | 256 | 1,000 ms |
| Extract, images | 90 | 512 | 3,000 ms |
| Extract, other inputs | 210 | 512 | 500 ms |
| Synthesize | 300 | 512 | 6,000 ms |
| PrepareApproval + Containment | 180 | 256 | 500 ms |

## 4. What Cost Explorer recorded

The daily `costs.csv` export is grouped by **Service**. It has 20 service/category columns and a total column. Its date rows run from **1 through 24 November 2026**. The reconciliation uses **1–23 November**, including the WAF test day. In this export the 24 November row has a zero total and empty service cells. November was still open.

| Reconciled item | Value in the export |
|---|---:|
| Report total, 1–23 November | −0.0000003837 USD |
| Daily total, 23 November | −0.0000000976 USD |
| WAF column, 23 November | −0.0000000730 USD |
| Bedrock column, 23 November | `-0` |
| Bedrock / Bedrock Managed Knowledge Base, period total | 0 USD / 0 USD |

Summing the 23 daily totals reproduces the export’s *Service total*. At cent precision the reported amount is **USD 0.00**. The file groups by service and does not record the selected cost metric, tag filters, token counts or credit breakdown. This is the **total within the exported report’s scope**. The exact project attribution and the reason for the tiny negative balance require further billing detail. [Download the relevant rows extracted from the report (CSV)](/downloads/phishguard-cost-observed.csv)

### Finish reconciliation from the billing account

- Reopen **Billing and Cost Management → Cost Explorer** with the same dates, **Daily → Group by Service → Unblended cost**. Include all regions so global services remain visible. Capture the date range, metric and filters. **Download CSV** is below the chart. Mask account names and identifiers in a public screenshot. [Export cost data](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-download-csv.html)
- Make a second view grouped by **Charge type**. Compare it with **Bills → November 2026 → Charges by service / Credits**. Record the usage charges, credits or refunds, and tax that actually appear. If the account is shared, use an activated cost allocation tag where available. Mark any unattributed amount as shared. Export again after month-end if a final statement is needed.
- To investigate Bedrock, open **CloudWatch → Metrics → AWS/Bedrock** in the calling region and select the model or inference profile. Check **Sum** for `Invocations`, `InputTokenCount` and `OutputTokenCount` over the same period. Compare timestamps with an incident’s Synthesize logs. The metrics describe usage. Bills and charge types explain the monetary adjustments. [Bedrock runtime metrics](https://docs.aws.amazon.com/bedrock/latest/userguide/monitoring-runtime-metrics.html)

## 5. Controlling costs while preserving evidence

- **WAF accounts for about 75% of the baseline.** Keep the probe only while testing and use the existing alarms to monitor failures. Add a paid dashboard when someone has a recurring need for it.
- **Measure AI and OCR at the step that incurs the charge.** Separate image and text cases when sampling Extract’s `Billed Duration`. For Synthesize, measure tokens and the number of cases that reach this step before changing model or context length. Include Guardrails and KB queries when comparing alternatives. [Lambda](https://aws.amazon.com/lambda/pricing/) · [Bedrock](https://aws.amazon.com/bedrock/pricing/) · [S3 Vectors](https://aws.amazon.com/s3/pricing/)
- **Clean up according to retention requirements.** Review log retention, older object versions and intake storage after the demo. Preserve the evidence retention period. Recalculate when new measurements of storage volume or OCR duration are available. [S3](https://aws.amazon.com/s3/pricing/) · [KMS](https://aws.amazon.com/kms/pricing/)

