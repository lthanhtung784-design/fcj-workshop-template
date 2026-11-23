---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu Tuần 7:

- Thiết kế sao lưu và phục hồi với AWS Backup và EBS Data Lifecycle Manager.
- Hiểu phục hồi sau thảm họa với Elastic Disaster Recovery.
- Nắm quy trình ứng phó sự cố khi lộ access key.
- Tìm hiểu xác thực người dùng ứng dụng với Amazon Cognito.

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Học module Data Protection with AWS Backup<br>- Tạo backup plan, vault và retention policy<br>- Thực hành sao lưu và kiểm thử khôi phục tài nguyên<br>- Tìm hiểu vault lock và sao chép sang tài khoản/region khác để chống ransomware | 26/10/2026 | 26/10/2026 | AWS Cloud Journey – Data Protection with AWS Backup<br>AWS Docs – AWS Backup Developer Guide |
| 2 | - Học module Snapshot Automation with Amazon EBS Data Lifecycle Manager<br>- Tạo lifecycle policy chụp snapshot theo lịch và giữ lại theo số lượng (by count)<br>- Học module Anomaly Detection for EBS Backups<br>- Ghi lại cách giám sát bản sao lưu để phát hiện sự cố sớm | 27/10/2026 | 27/10/2026 | AWS Cloud Journey – Snapshot Automation with Amazon EBS Data Lifecycle Manager<br>AWS Cloud Journey – Anomaly Detection for EBS Backups<br>AWS Docs – Amazon Data Lifecycle Manager |
| 3 | - Học module Disaster Recovery with AWS Elastic Disaster Recovery<br>- Phân biệt RPO, RTO và các chiến lược DR<br>- Tìm hiểu continuous replication, diễn tập (drills) và phục hồi<br>- So sánh Elastic Disaster Recovery với sao lưu thông thường | 28/10/2026 | 28/10/2026 | AWS Cloud Journey – Disaster Recovery with AWS Elastic Disaster Recovery<br>AWS Docs – AWS Elastic Disaster Recovery User Guide |
| 4 | - Nghiên cứu quy trình xử lý khi lộ AWS access key trên GitHub<br>- Hiểu rằng AWS gắn quarantine policy nhưng không tự vô hiệu hóa key<br>- Tóm tắt các bước: chuyển key sang Inactive, thay credentials mới, điều tra bằng CloudTrail, rà soát tài khoản<br>- Viết bài chia sẻ kiến thức cho nhóm học tập | 29/10/2026 | 29/10/2026 | AWS Security Blog – What to do if you inadvertently expose an AWS access key (<https://aws.amazon.com/blogs/security/what-to-do-if-you-inadvertently-expose-an-aws-access-key>)<br>AWS re:Post – How AWS responds to exposed credentials (<https://repost.aws/articles/ARoBXj63rWSt2Ww7XKlVV72g/how-aws-responds-to-exposed-credentials-and-how-you-can-protect-your-account>)<br>Unit 42 – Detecting exposed AWS IAM credentials (<https://unit42.paloaltonetworks.com/detecting-exposed-aws-iam-credentials/>)<br>GitHub Docs – Secret scanning and push protection (<https://docs.github.com/en/code-security/secret-scanning/working-with-secret-scanning-and-push-protection>)<br>AWS Labs – git-secrets (<https://github.com/awslabs/git-secrets>) |
| 5 | - Học module Cross-Domain Authentication with Amazon Cognito<br>- Phân biệt user pools và identity pools<br>- Tìm hiểu OAuth 2.0/OIDC, hosted UI và MFA cho người dùng ứng dụng<br>- Ghi lại các lỗi cấu hình phổ biến | 30/10/2026 | 30/10/2026 | AWS Cloud Journey – Cross-Domain Authentication with Amazon Cognito<br>AWS Docs – Amazon Cognito Developer Guide |

### Kết quả đạt được trong Tuần 7:

- Hiểu bản sao lưu chỉ có giá trị khi đi kèm retention policy, chống xóa nhầm và kiểm thử khôi phục định kỳ.
- Phân biệt được backup với disaster recovery và nắm khái niệm RPO/RTO.
- Nắm quy trình ứng phó sự cố lộ access key và hoàn thành bài chia sẻ.
- Hiểu cách Cognito xác thực người dùng ứng dụng và điểm khác biệt so với IAM.