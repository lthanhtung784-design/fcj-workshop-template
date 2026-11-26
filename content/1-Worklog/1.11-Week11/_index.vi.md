---
title: "Worklog Tuần 11"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu Tuần 11:

- Hoàn thiện thiết kế kiến trúc workshop PhishGuard và tài liệu luồng xử lý sự cố đầu-cuối cho bài nộp.
- Triển khai và cấu hình các thành phần serverless cốt lõi của PhishGuard (S3 bucket **evidence**/**sanitized**, luồng phê duyệt Step Functions và tổng hợp playbook bằng Bedrock).
- Kiểm thử luồng tiếp nhận sự cố, trích xuất OCR/che PII, chấm điểm Triage và callback phê duyệt của SecOps ở chế độ `DRY_RUN`.
- Cập nhật tài liệu workshop trên Hugo, kiểm tra hiển thị sơ đồ kiến trúc và hoàn thiện bài nộp.

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Hoàn thiện sơ đồ kiến trúc PhishGuard (draw.io, XML, SVG, PNG) và tài liệu theo dấu sự cố<br>- Rà soát cấu hình S3 Object Lock chế độ Governance, mã hóa SSE-KMS và tách biệt hai bucket **evidence** và **sanitized**<br>- Thiết kế luồng callback phê duyệt thủ công bằng task token của Step Functions | 23/11/2026 | 23/11/2026 | AWS Docs – AWS Step Functions Callback Pattern<br>AWS Docs – Amazon S3 Object Lock Overview |
| 2 | - Triển khai và kiểm thử hai hàm Lambda Ingest và Extract & Redact<br>- Kiểm tra tính mã băm SHA-256 cho bằng chứng gốc, nhận diện chữ Tesseract tiếng Việt/Anh và che dữ liệu nhạy cảm (PII)<br>- Kiểm thử nhánh chuyển sang `NEEDS_MORE_INFO` khi ảnh thiếu chữ và không có chỉ báo QR hợp lệ | 24/11/2026 | 24/11/2026 | AWS Docs – AWS Lambda Developer Guide<br>Tài liệu kiến trúc và triển khai PhishGuard Workshop |
| 3 | - Cấu hình chấm điểm luật Triage, đối chiếu IOC và tổng hợp playbook qua Amazon Bedrock kèm cơ chế fallback<br>- Kiểm thử phân nhánh `PENDING_APPROVAL`, `NEEDS_REVIEW` và `NO_ACTION`<br>- Xác minh luồng phê duyệt ở chế độ `DRY_RUN` và lưu vết audit trên DynamoDB | 25/11/2026 | 25/11/2026 | AWS Docs – Amazon Bedrock User Guide<br>AWS Docs – Amazon DynamoDB Developer Guide |
| 4 | - Rà soát các trạng thái vòng đời sự cố (`NEEDS_MORE_INFO`, `NEEDS_REVIEW`, `NO_ACTION`, `PENDING_APPROVAL`, `REJECTED`, `ESCALATED_TIMEOUT`) và bản ghi audit trên DynamoDB<br>- Kiểm tra chế độ duyệt `DRY_RUN` và phạm vi blocklist nội bộ<br>- Chỉnh sửa nội dung song ngữ (`en`/`vi`) trang theo dấu sự cố và định dạng hiển thị | 26/11/2026 | 26/11/2026 | AWS Docs – Step Functions `SendTaskSuccess`<br>Tài liệu luồng sự cố PhishGuard Workshop |
| 5 | - Cập nhật trang tài liệu Hugo (`fcj-workshop-template`) với nội dung song ngữ (`en`/`vi`) và sơ đồ kiến trúc PhishGuard<br>- Sửa lỗi đường dẫn tương đối cho thư mục con trên GitHub Pages và các liên kết tải tài nguyên tĩnh<br>- Tổng hợp tiến độ Tuần 11 và hoàn thiện bài nộp workshop | 27/11/2026 | 27/11/2026 | Hugo Documentation – URL Management<br>FCAJ Worklog Tuần 1–11 |

### Kết quả đạt được trong Tuần 11:

- Hoàn thiện kiến trúc PhishGuard và tài liệu vòng đời xử lý sự cố kèm đầy đủ các định dạng sơ đồ `.drawio`, `.xml` và `.svg`.
- Kiểm thử thành công cơ chế bảo toàn bằng chứng (SHA-256, S3 Object Lock), che PII, tổng hợp playbook bằng Bedrock có fallback và luồng phê duyệt qua Step Functions.
- Cập nhật và triển khai thành công nội dung workshop song ngữ cùng các tệp sơ đồ lên GitHub Pages, sẵn sàng cho bài nộp.