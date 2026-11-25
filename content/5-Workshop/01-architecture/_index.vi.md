---
title: "Theo dấu một sự cố"
weight: 1
chapter: false
---

![PhishGuard AWS architecture with evidence storage and an approval callback](/images/phishguard/PhishGuard-Architecture.png)

[draw.io](/downloads/PhishGuard-Architecture.drawio) · [XML](/downloads/PhishGuard-Architecture.xml) · [SVG](/images/phishguard/architecture.svg)

1. Trình duyệt tải React qua CloudFront, đăng nhập Cognito và gửi JWT đến HTTP API. Reporter API và Admin API đọc/ghi DynamoDB để tra hồ sơ, kiểm quyền và ghi quyết định.
2. Với ảnh hoặc EML, trình duyệt nhận form ký rồi POST trực tiếp đến S3. Với văn bản và mẫu demo, Reporter API ghi hoặc sao chép file. Cả ba đường web tạo `uploads/{uuid}/raw`, sự kiện S3 gọi Ingest. Email đi đường riêng: SES lưu MIME vào `inbound/` rồi gọi Ingest kèm thông tin xác thực lần nhận.
3. Ingest kiểm dữ liệu, tính SHA-256 và ghi bản gốc vào bucket **evidence**, có versioning, SSE-KMS và Object Lock Governance 7 ngày. Sau khi lưu thành công, Ingest mở execution mang tên incident, truyền tham chiếu gồm `raw_s3_key`, `raw_s3_version_id` khi có và `evidence_sha256`. Bucket **sanitized** lưu riêng bản phân tích đã che PII. DLQ nhận các lần gọi Ingest bất đồng bộ đã thất bại sau retry.
4. Extract & Redact đọc bản gốc, dùng Tesseract tiếng Việt/Anh cho ảnh và che PII. Ảnh thiếu chữ đi tới `NEEDS_MORE_INFO`. Triage chấm theo luật và đối chiếu IOC. Synthesize truy xuất playbook và gọi Bedrock khi đã cấu hình. Khi tổng hợp lỗi, trang sự cố hiện `FALLBACK` và kết quả theo luật.
5. Thiếu hành động phù hợp: HIGH/CRITICAL chuyển `NEEDS_REVIEW` và báo SNS, mức thấp hơn thành `NO_ACTION`. Có đề xuất: PrepareApproval **ghi token và trạng thái `PENDING_APPROVAL` trước**, sau đó gửi SNS. Step Functions giữ bước chờ. Lambda kết thúc lượt gọi.
6. Admin quyết định trên web. Admin API kiểm quyền, kiểm trạng thái rồi gửi `SendTaskSuccess` mang kết quả về workflow. Từ chối thành `REJECTED`, quá hạn thành `ESCALATED_TIMEOUT`. Duyệt ở chế độ `DRY_RUN` ghi kết quả mô phỏng và audit; mục blocklist nếu có chỉ có hiệu lực trong ứng dụng.


