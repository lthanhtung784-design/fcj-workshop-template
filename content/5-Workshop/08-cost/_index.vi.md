---
title: "COST · Dự toán và chi phí quan sát"
weight: 8
chapter: false
---

Với **300 báo cáo trong 30 ngày**, chi phí dịch vụ dự kiến của PhishGuard là **9,37 USD/tháng**, trước thuế và phí gia hạn tên miền. Dữ liệu Cost Explorer ngày **01–23/11/2026** cho kết quả **0,00 USD** khi làm tròn đến cent. Dự toán giả định WAF hoạt động đủ tháng. Trong kỳ đo, ngày 23/11 mới có phép thử WAF được lưu làm minh chứng. Hai con số trả lời hai câu hỏi khác nhau: cần dự trù bao nhiêu để duy trì hệ thống và báo cáo tài khoản đã ghi nhận bao nhiêu trong kỳ lab.

## 1. Phạm vi của dự toán

Ứng dụng chạy ở **US East (N. Virginia), `us-east-1`**, với CloudFront **Pay-as-you-go**. Web ACL `PhishGuardEdge` bảo vệ distribution. Mô hình dùng một AWS managed rule group tiêu chuẩn và một rate-based rule. Probe dùng để chứng minh 403 đã tắt trong cấu hình cuối. Hai alarm theo dõi workflow thất bại và hàng đợi lỗi của Ingest. Việc xem biểu đồ WAF trên console không tạo thêm một custom metric trong dự toán này.

Giả định tải gồm **90 ảnh, 60 email đến qua SES và 90 ca đi đến bước quyết định** trong tổng số 300 báo cáo. Các nhóm này có thể giao nhau. Portal phát sinh 12.000 HTTP API request và distribution phục vụ 20.000 HTTPS request, 1 GB tới người xem. Để dự trù phần AI, mô hình tính một lượt tổng hợp và một truy vấn KB cho mỗi báo cáo. Thực tế có ca dừng sớm vì thiếu bằng chứng. File POST trực tiếp tới S3 không đi qua WAF.

## 2. Bảng tính cho một tháng

| Khoản | Đầu vào chính | USD/tháng |
|---|---|---:|
| AWS WAF | 1 ACL × 5 USD + 1 managed group × 1 USD + 1 rate rule × 1 USD + 0,02 triệu request × 0,60 USD | 7,0120 |
| CloudFront | PAYG, 1 GB và 20.000 request nằm trong hạn mức còn lại của tài khoản | 0,0000 |
| AWS KMS | 1 khóa đối xứng do khách hàng quản lý, 2.400 request | 1,0072 |
| Route 53 | Giả định phân bổ riêng 1 public hosted zone và 1.000 truy vấn DNS chuẩn | 0,5004 |
| CloudWatch | 2 alarm tiêu chuẩn, mỗi alarm 1 metric, nạp 0,1 GB log và giữ 0,05 GB-tháng | 0,2515 |
| Lambda và HTTP API | 13.380 lần gọi Lambda x86, 1.860 GB-giây, 12.000 HTTP API request | 0,0457 |
| Step Functions Standard | 300 execution × 12 lần chuyển trạng thái × 0,000025 USD | 0,0900 |
| Bedrock Nova Lite v1 | 0,6 triệu token vào × 0,06 USD + 0,3 triệu token ra × 0,24 USD | 0,1080 |
| Guardrails và Titan Text Embeddings V2 | 1.800 text unit chịu phí cho content filter, 130.000 token embedding cho đồng bộ và truy vấn | 0,2726 |
| S3 Standard và S3 Vectors | 1 GB-tháng, 1.500 lượt ghi và 6.000 lượt đọc S3. Vector lưu và ghi 0,01 GB mỗi loại, 300 truy vấn nhỏ | 0,0363 |
| DynamoDB | On-demand, 6.000 đơn vị ghi, 30.000 đơn vị đọc, 0,05 GB-tháng lưu và 0,05 GB-tháng PITR | 0,0300 |
| SES, SNS và SQS | 60 thư đến + 60 chunk chịu phí, 90 publish và 90 email thông báo, 1.000 request SQS | 0,0136 |
| Cognito và Budgets | 10 người dùng đăng nhập trực tiếp trong hạn mức đủ điều kiện, giả định 1 cost budget chỉ gửi thông báo | 0,0000 |
| **Tổng tính trước khi làm tròn từng dòng** | **Chưa gồm domain và thuế** | **9,37** |

Bảng lấy biểu WAF theo ACL/rule áp dụng cho kỳ workshop tháng 11/2026. Khi dùng Calculator, đối chiếu **kỳ áp dụng của giá**. Nếu tài khoản được tính theo số tài nguyên bảo vệ, với 1 distribution × 720 giờ × 0,01 USD và cùng lượng request, thay dòng WAF bằng **7,212 USD**. Khi đó tổng là **9,57 USD**. Phí cố định của biểu ACL/rule được phân bổ theo giờ, kể cả probe trong thời gian thử. [Biểu giá AWS WAF và thời điểm áp dụng](https://aws.amazon.com/waf/pricing/)

Bảng sử dụng giá niêm yết cho phần lớn dịch vụ, dành riêng hai giả định về hạn mức cho CloudFront và Cognito. Credit, ưu đãi còn lại, phí truy vấn Billing và thuế phụ thuộc tài khoản. Nếu DNS dùng chung và không phân bổ phần nào cho lab, tổng cơ sở còn **8,87 USD**. Nếu thực sự dùng thêm một dashboard trả phí và một custom metric, cộng khoảng **3,30 USD/tháng** theo giá niêm yết để ra **12,67 USD**. Phí tên miền quy đổi theo **giá gia hạn thực tế mỗi năm ÷ 12**. [CloudFront PAYG](https://aws.amazon.com/cloudfront/faqs/) · [CloudWatch](https://aws.amazon.com/cloudwatch/pricing/) · [Route 53](https://aws.amazon.com/route53/pricing/)

[Tải bảng tính từng đơn vị và nguồn giá (CSV)](/downloads/phishguard-cost-inputs.csv)

## 3. Lập lại dự toán trong AWS Pricing Calculator

1. Mở **AWS Pricing Calculator → Create estimate → Add service**. Đặt nhóm `PhishGuard | 300 reports`. Chọn **US East (N. Virginia)** cho các dịch vụ theo vùng. Với CloudFront, chọn PAYG và khu vực người xem phù hợp.
2. Nhập WAF, KMS, CloudWatch và Route 53 trước. Riêng WAF có **một** managed group tiêu chuẩn và **một** rate rule. Giữ probe ở 0. Với ô yêu cầu tính theo triệu, 20.000 request nhập **0.02**. Nhập tiếp các dịch vụ còn lại theo bảng và CSV.
3. Với Lambda, chọn **on-demand, x86**. Tách thành sáu dòng dưới đây khi ô nhập yêu cầu một cặp RAM và thời gian. OCR Tesseract và giải mã QR đã nằm trong thời gian chạy Extract. Step Functions giữ trạng thái chờ phê duyệt, nên thời gian chờ 48 giờ không được cộng vào thời lượng Lambda.
4. Với Bedrock, chọn **Amazon Nova Lite v1**, on-demand. Nhập **300** lượt/tháng, mỗi lượt **2.000 input token, 1.000 output token**, hoặc nhập trực tiếp **600.000/300.000** token tháng theo giao diện. Với dịch vụ hay bộ lọc chưa có ô tương ứng, ghi riêng số tiền tính tay từ CSV. Tổng trình bày bằng subtotal Calculator cộng các dòng thủ công chưa được tính.
5. Ở **My Estimate**, dùng **Share/Save** và xuất PDF. Đặt link hoặc PDF cạnh bảng. Ghi rõ Calculator có áp dụng hạn mức miễn phí nào và dòng nào cộng tay nếu tổng khác 9,37 USD. [AWS Pricing Calculator](https://calculator.aws/) · [Cách lưu và chia sẻ](https://docs.aws.amazon.com/pricing-calculator/latest/userguide/save-share-estimate.html)

| Dòng Lambda | Lần/tháng | MiB | Thời lượng giả định mỗi lần |
|---|---:|---:|---:|
| Reporter API + Admin API | 12.000 | 256 | 200 ms |
| Ingest + Triage | 600 | 256 | 1.000 ms |
| Extract trên ảnh | 90 | 512 | 3.000 ms |
| Extract các đầu vào khác | 210 | 512 | 500 ms |
| Synthesize | 300 | 512 | 6.000 ms |
| PrepareApproval + Containment | 180 | 256 | 500 ms |

## 4. Dữ liệu Cost Explorer của kỳ chạy lab

File `costs.csv` xuất theo ngày và nhóm theo **Service**, có 20 cột dịch vụ/hạng mục và một cột tổng. File chứa các dòng **01–24/11/2026**. Bảng đối chiếu dùng **01–23/11** để bao gồm ngày thử WAF. Dòng 24/11 có tổng 0 và các ô dịch vụ trống trong lần xuất này. Tháng 11 vẫn đang mở.

| Dòng được đối chiếu | Kết quả đọc từ CSV |
|---|---:|
| Tổng báo cáo từ 01–23/11 | −0,0000003837 USD |
| Tổng riêng ngày 23/11 | −0,0000000976 USD |
| Cột WAF ngày 23/11 | −0,0000000730 USD |
| Cột Bedrock ngày 23/11 | `-0` |
| Bedrock / Bedrock Managed Knowledge Base cả kỳ | 0 USD / 0 USD |

Cộng 23 giá trị ngày được đúng bằng dòng *Service total* của file. Khi báo cáo đến cent, tổng là **0,00 USD**. File nhóm theo dịch vụ, không ghi bộ lọc tag, chỉ số chi phí đã chọn, số token hay chi tiết credit. Vì vậy, workshop ghi đây là **tổng trong phạm vi báo cáo đã xuất**. Chi phí tách riêng cho PhishGuard và nguyên nhân số dư âm rất nhỏ vẫn cần đối chiếu Billing. [Tải các dòng dùng để đối chiếu (CSV trích từ báo cáo)](/downloads/phishguard-cost-observed.csv)

### Chốt phần chỉ chủ tài khoản nhìn thấy

- Mở lại **Billing and Cost Management → Cost Explorer**, chọn cùng kỳ, **Daily → Group by Service → Unblended cost**. Giữ tất cả region để thấy cả dịch vụ global. Lưu ảnh có ngày, metric và bộ lọc. Bảng dưới biểu đồ có nút **Download CSV**. Khi chia sẻ, có thể che tên tài khoản và mã định danh. [Hướng dẫn xuất CSV](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-download-csv.html)
- Tạo một góc nhìn thứ hai **Group by → Charge type** và đối chiếu với **Bills → November 2026 → Charges by service / Credits**. Ghi usage trước điều chỉnh, credit/refund và thuế theo những dòng thực sự xuất hiện. Với tài khoản dùng chung, dùng tag phân bổ chi phí đã được kích hoạt nếu có. Nếu không thể phân bổ một khoản, ghi là chi phí dùng chung. Xuất lại sau khi tháng đóng sổ nếu cần số cuối kỳ.
- Để giải thích riêng Bedrock, mở **CloudWatch → Metrics → AWS/Bedrock** ở vùng gọi model, chọn đúng model hoặc inference profile. Đọc **Sum** của `Invocations`, `InputTokenCount` và `OutputTokenCount` trong cùng kỳ. Đối chiếu thời điểm với log Synthesize của một incident. Các metric giúp xác nhận lượng gọi. Bills và Charge type mới cho biết số tiền và khoản điều chỉnh. [Metric Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/monitoring-runtime-metrics.html)

## 5. Tối ưu chi phí mà vẫn giữ được bằng chứng

- **WAF chiếm khoảng 75% mức cơ sở.** Với lab ít request, giữ probe trong thời gian kiểm thử cần thiết và dùng alarm đã có để theo dõi lỗi. Chỉ thêm dashboard trả phí khi có người sử dụng thường xuyên.
- **Đo AI và OCR ở đúng bước.** Tách ảnh khỏi văn bản khi đo `Billed Duration` của Extract. Với Synthesize, đo token thực tế và số ca thật sự tới bước này trước khi chỉnh độ dài ngữ cảnh hoặc đổi model. Hai lớp kiểm soát dễ bị tính sót là Guardrails và truy vấn KB. [Lambda](https://aws.amazon.com/lambda/pricing/) · [Bedrock](https://aws.amazon.com/bedrock/pricing/) · [S3 Vectors](https://aws.amazon.com/s3/pricing/)
- **Dọn theo vòng đời dữ liệu.** Kiểm tra log retention, các phiên bản object cũ và bucket intake sau demo. Giữ thời hạn bảo toàn bằng chứng của bucket evidence. So sánh lại dự toán khi có số đo dung lượng hoặc thời lượng OCR mới. [S3](https://aws.amazon.com/s3/pricing/) · [KMS](https://aws.amazon.com/kms/pricing/)

