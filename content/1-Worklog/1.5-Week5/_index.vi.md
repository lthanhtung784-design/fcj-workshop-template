---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu Tuần 5:

- Làm chủ IAM policies nâng cao: conditions và logic đánh giá quyền.
- Hiểu IAM Permission Boundaries để phân quyền mà không leo thang đặc quyền.
- Sử dụng AWS SSO (IAM Identity Center) thay cho IAM users dài hạn.
- Hiểu mã hóa với KMS và quản lý bí mật (secrets) với Secrets Manager.

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Học module Access Control with IAM Policies and Conditions<br>- Tìm hiểu logic đánh giá policy: mặc định từ chối (default deny), explicit deny luôn thắng<br>- Thực hành điều kiện aws:MultiFactorAuthPresent, aws:SourceIp và aws:RequestedRegion<br>- Kiểm tra bằng Policy Simulator và ghi lại các trường hợp có quyền nhưng vẫn bị từ chối | 12/10/2026 | 12/10/2026 | AWS Cloud Journey – Access Control with IAM Policies and Conditions<br>AWS Docs – Policy evaluation logic<br>AWS Docs – Security best practices in IAM (<https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html>) |
| 2 | - Học module Permission Management with IAM Permission Boundaries<br>- Hiểu rủi ro leo thang đặc quyền khi cho phép tạo role/user<br>- Tạo permission boundary, gắn vào delegated user và so sánh hành vi trước/sau<br>- Tóm tắt mối quan hệ giữa identity policies, boundaries và SCPs | 13/10/2026 | 13/10/2026 | AWS Cloud Journey – Permission Management with IAM Permission Boundaries<br>AWS Docs – Permissions boundaries for IAM entities |
| 3 | - Học module Identity Federation with AWS Single Sign-On<br>- Tìm hiểu IAM Identity Center, permission sets và gán quyền theo group<br>- Đăng nhập CLI bằng SSO (aws configure sso) và so sánh với access keys dài hạn<br>- Đánh giá lợi ích bảo mật: temporary credentials và MFA tập trung | 14/10/2026 | 14/10/2026 | AWS Cloud Journey – Identity Federation with AWS Single Sign-On<br>AWS Docs – AWS IAM Identity Center User Guide |
| 4 | - Học module Encryption with AWS Key Management Service (KMS)<br>- Phân biệt AWS managed keys và customer managed keys; tìm hiểu envelope encryption và key rotation<br>- Tìm hiểu cách key policies phối hợp với IAM policies<br>- Mã hóa S3 bucket hoặc EBS volume bằng KMS và kiểm thử quyền kms:Decrypt | 15/10/2026 | 15/10/2026 | AWS Cloud Journey – Encryption with AWS Key Management Service (KMS)<br>AWS Docs – AWS KMS Developer Guide |
| 5 | - Học module Credentials Management with AWS Secrets Manager<br>- Lưu thông tin kết nối database dưới dạng secret và truy xuất qua CLI/SDK<br>- Tìm hiểu cơ chế tự động xoay vòng (automatic rotation)<br>- So sánh với Systems Manager Parameter Store và lưu ý chi phí tính theo từng secret | 16/10/2026 | 16/10/2026 | AWS Cloud Journey – Credentials Management with AWS Secrets Manager<br>AWS Docs – AWS Secrets Manager User Guide |

### Kết quả đạt được trong Tuần 5:

- Hiểu vì sao có Allow nhưng vẫn bị Deny (explicit deny, boundaries, key policies) và cách kiểm tra bằng Policy Simulator.
- Hiểu cách permission boundary giới hạn trần quyền khi phân quyền.
- Dùng SSO để cấp credential tạm thời thay cho access keys dài hạn.
- Hiểu rằng mã hóa KMS không thay thế kiểm soát truy cập: ai được phép decrypt vẫn có thể đọc dữ liệu.
- Biết lưu secrets vào Secrets Manager thay vì hard-code trong mã nguồn.