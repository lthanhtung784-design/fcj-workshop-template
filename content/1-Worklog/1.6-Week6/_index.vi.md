---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu Tuần 6:

- Hiểu ghi nhật ký và điều tra với CloudTrail.
- Phát hiện mối đe dọa với GuardDuty và gửi cảnh báo qua EventBridge/SNS.
- Đánh giá tuân thủ cấu hình với Security Hub.
- Tìm hiểu bảo vệ ứng dụng web với AWS WAF, Macie và Firewall Manager.

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Học AWS CloudTrail: Event history vs trails, management events vs data events<br>- Hiểu rằng CloudTrail data events không được ghi mặc định mà cần cấu hình thêm<br>- Tìm hiểu log file validation và gửi log về bucket chuyên dụng<br>- Thực hành lookup-events để tìm hoạt động theo access key hoặc user | 19/10/2026 | 19/10/2026 | AWS Cloud Journey – S3 Security Best Practices<br>AWS Docs – AWS CloudTrail User Guide<br>AWS Docs – Logging data events |
| 2 | - Học module Threat Detection with AWS GuardDuty<br>- Bật GuardDuty và S3 Protection; tìm hiểu các loại finding (ví dụ Exfiltration:S3/AnomalousBehavior)<br>- Tạo sample findings để quan sát kết quả mà không giả lập tấn công thật<br>- Kết nối GuardDuty → EventBridge → SNS → Email và kiểm thử luồng cảnh báo | 20/10/2026 | 20/10/2026 | AWS Cloud Journey – Threat Detection with AWS GuardDuty<br>AWS Docs – Amazon GuardDuty User Guide<br>AWS Docs – Generating sample findings |
| 3 | - Học module Security Compliance with AWS Security Hub<br>- Bật Security Hub với chuẩn AWS Foundational Security Best Practices<br>- Đọc findings, mức độ nghiêm trọng (severity) và điểm tuân thủ (compliance score)<br>- Lưu ý chi phí và tắt dịch vụ sau khi thực hành | 21/10/2026 | 21/10/2026 | AWS Cloud Journey – Security Compliance with AWS Security Hub<br>AWS Docs – AWS Security Hub User Guide |
| 4 | - Học module Application Protection with AWS WAF<br>- Tìm hiểu web ACLs, managed rule groups và rate-based rules<br>- Dùng chế độ Count để kiểm thử rule trước khi chuyển sang Block<br>- Nhận diện giới hạn của WAF: không thay thế việc viết code an toàn và vá ứng dụng | 22/10/2026 | 22/10/2026 | AWS Cloud Journey – Application Protection with AWS WAF<br>AWS Docs – AWS WAF Developer Guide |
| 5 | - Học module Data Protection with Amazon Macie<br>- Tìm hiểu cách Macie phát hiện dữ liệu nhạy cảm (PII) trên S3<br>- Học module Security Governance with AWS Firewall Manager<br>- Hiểu cách quản lý tập trung WAF và Security Group qua AWS Organizations; lưu ý chi phí | 23/10/2026 | 23/10/2026 | AWS Cloud Journey – Data Protection with Amazon Macie<br>AWS Cloud Journey – Security Governance with AWS Firewall Manager<br>AWS Docs – Amazon Macie User Guide<br>AWS Docs – AWS Firewall Manager |

### Kết quả đạt được trong Tuần 6:

- Phân biệt được vai trò từng dịch vụ: CloudTrail (ai làm gì), GuardDuty (hành vi bất thường), Security Hub (tuân thủ cấu hình), WAF (lọc request web).
- Xây dựng luồng cảnh báo GuardDuty → EventBridge → SNS → Email bằng sample findings.
- Hiểu cần cấu hình data events để điều tra hoạt động ở cấp độ đối tượng (object-level).
- Biết đánh giá chi phí và tắt các dịch vụ tính phí sau khi thực hành.
- Hiểu rằng một finding không hẳn là đã bị xâm nhập và cần kiểm tra bằng chứng trước.