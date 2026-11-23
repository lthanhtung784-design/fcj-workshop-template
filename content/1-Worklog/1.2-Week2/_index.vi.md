---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu Tuần 2:

- Hiểu mô hình IAM (users, groups, roles, policies) và nguyên tắc đặc quyền tối thiểu (least-privilege).
- Bảo vệ tài khoản bằng MFA và tránh dùng tài khoản root cho công việc hằng ngày.
- Nắm kiến thức mạng VPC cơ bản: subnets, route tables, Internet Gateway, NAT Gateway, Security Groups, NACLs.
- Khởi chạy EC2 an toàn và dùng IAM roles thay vì access keys dài hạn.

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Học module Access Management with AWS IAM<br>- Phân biệt root user, IAM users, groups, roles và policies<br>- Tìm hiểu cấu trúc JSON policy (Effect, Action, Resource, Condition) và nguyên tắc least-privilege<br>- Đọc Shared Responsibility Model và các thực hành bảo mật tốt nhất cho IAM | 21/09/2026 | 21/09/2026 | AWS Cloud Journey – Access Management with AWS IAM<br>AWS Docs – Security best practices in IAM (<https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html>)<br>AWS – Shared Responsibility Model (<https://aws.amazon.com/compliance/shared-responsibility-model/>) |
| 2 | - Bật MFA cho root user và tạo admin IAM user để thay thế root trong công việc hằng ngày<br>- Tạo group, gắn managed policies và viết customer managed policy giới hạn theo tài nguyên cụ thể<br>- Dùng IAM Policy Simulator để kiểm tra quyền hiệu lực<br>- Ghi lại kết quả và các lỗi AccessDenied gặp phải | 22/09/2026 | 22/09/2026 | AWS Cloud Journey – Access Management with AWS IAM<br>AWS Docs – IAM Policy Simulator |
| 3 | - Học module Networking Essentials with Amazon VPC<br>- Tìm hiểu public/private subnets, route tables, Internet Gateway và NAT Gateway<br>- So sánh Security Groups (stateful) với Network ACLs (stateless)<br>- Tạo VPC có public subnet và private subnet, kiểm tra route tables | 23/09/2026 | 23/09/2026 | AWS Cloud Journey – Networking Essentials with Amazon VPC<br>AWS Docs – Amazon VPC User Guide |
| 4 | - Học module Compute Essentials with Amazon EC2<br>- Khởi chạy EC2 instance trong public subnet với key pair và Security Group chỉ cho phép SSH từ IP cá nhân<br>- Kết nối qua SSH và kiểm tra cấu hình<br>- Tìm hiểu instance types, EBS và cách tính giá; stop/terminate tài nguyên sau khi thực hành | 24/09/2026 | 24/09/2026 | AWS Cloud Journey – Compute Essentials with Amazon EC2<br>AWS Docs – Amazon EC2 User Guide |
| 5 | - Học module Instance Profiling with IAM Roles for EC2<br>- Tạo IAM role và instance profile có quyền đọc S3 rồi gắn vào EC2<br>- Truy cập S3 từ EC2 bằng AWS CLI mà không dùng access key<br>- Tìm hiểu về temporary credentials và Instance Metadata Service (IMDS) | 25/09/2026 | 25/09/2026 | AWS Cloud Journey – Instance Profiling with IAM Roles for EC2<br>AWS Docs – IAM roles for Amazon EC2 |

### Kết quả đạt được trong Tuần 2:

- Hiểu cách IAM kiểm soát ai được làm gì trên tài nguyên nào và lý do chỉ nên dùng root user khi thật sự cần thiết.
- Thực hành bật MFA, tạo admin IAM user, viết policy giới hạn quyền và kiểm thử bằng Policy Simulator.
- Nắm cấu trúc VPC cơ bản và sự khác nhau giữa Security Groups và Network ACLs.
- Khởi chạy EC2 có giới hạn SSH bằng Security Group và dọn dẹp tài nguyên sau khi thực hành.
- Hiểu vì sao IAM roles (temporary credentials) được ưu tiên hơn access keys dài hạn.