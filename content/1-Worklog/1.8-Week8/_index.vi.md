---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu Tuần 8:

- Tự động hóa vận hành với Lambda dùng execution role theo nguyên tắc least-privilege.
- Quản lý hạ tầng dưới dạng mã (IaC) với CloudFormation và CDK.
- Tìm hiểu vá hệ thống với EC2 Image Builder.
- Hiểu các kiến trúc web có tính sẵn sàng cao (highly available).

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Học module Serverless Automation with AWS Lambda<br>- Tạo Lambda function đầu tiên với execution role chỉ chứa quyền cần thiết<br>- Cấu hình trigger (EventBridge hoặc S3) và xem log trên CloudWatch<br>- Tìm hiểu rủi ro khi gắn role quá rộng cho Lambda | 02/11/2026 | 02/11/2026 | AWS Cloud Journey – Serverless Automation with AWS Lambda<br>AWS Docs – AWS Lambda Developer Guide |
| 2 | - Học module Infrastructure as Code with AWS CloudFormation<br>- Viết template tạo VPC, Security Group hoặc EC2 và triển khai dưới dạng stack<br>- Tìm hiểu parameters, change sets và drift detection<br>- Dọn dẹp bằng cách xóa stack | 03/11/2026 | 03/11/2026 | AWS Cloud Journey – Infrastructure as Code with AWS CloudFormation<br>AWS Docs – AWS CloudFormation User Guide |
| 3 | - Học module Cloud Development Kit (AWS CDK) Essentials<br>- Khởi tạo dự án CDK và tìm hiểu constructs, stacks, synth và deploy<br>- So sánh CDK với CloudFormation<br>- Ghi nhận lợi ích của IaC: lặp lại được, dễ review, ít sai cấu hình | 04/11/2026 | 04/11/2026 | AWS Cloud Journey – Cloud Development Kit (AWS CDK) Essentials<br>AWS Docs – AWS CDK Developer Guide |
| 4 | - Học module Systems Patching with EC2 Image Builder<br>- Tạo image pipeline và recipe để build AMI chuẩn<br>- Liên hệ với Systems Manager Patch Manager và trách nhiệm của khách hàng trong việc vá OS trên EC2<br>- Ghi lại quy trình làm mới AMI định kỳ | 05/11/2026 | 05/11/2026 | AWS Cloud Journey – Systems Patching with EC2 Image Builder<br>AWS Docs – EC2 Image Builder User Guide |
| 5 | - Học các module Scaling Applications with EC2 Auto Scaling và Building Highly Available Web Applications<br>- Thiết kế kiến trúc với ALB + Auto Scaling + Multi-AZ + RDS Multi-AZ<br>- Xác định Security Groups cho từng tầng (ALB, application, database)<br>- Xóa tài nguyên sau khi thực hành | 06/11/2026 | 06/11/2026 | AWS Cloud Journey – Scaling Applications with EC2 Auto Scaling<br>AWS Cloud Journey – Building Highly Available Web Applications<br>AWS Docs – Amazon EC2 Auto Scaling User Guide |

### Kết quả đạt được trong Tuần 8:

- Cấp quyền tối thiểu cho Lambda và hiểu rủi ro của các role quá rộng.
- Triển khai hạ tầng bằng CloudFormation/CDK và hiểu lợi ích về tính nhất quán, dễ review.
- Hiểu vai trò của AMI chuẩn và việc vá định kỳ cho workload trên EC2.
- Thiết kế được kiến trúc web sẵn sàng cao với phân lớp Security Group hợp lý.