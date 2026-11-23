---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu Tuần 3:

- Lưu trữ website tĩnh trên S3 và hiểu các thiết lập bảo mật quan trọng của S3.
- Sử dụng AWS CLI với profiles để thao tác an toàn và lặp lại được.
- Thiết lập giám sát và cảnh báo cơ bản với CloudWatch.
- Hiểu cách triển khai RDS trong private subnet.

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Học module Static Website Hosting with Amazon S3<br>- Tạo bucket, bật static website hosting và tải lên file index.html<br>- Cấu hình bucket policy cho phép public read chỉ ở nơi cần thiết<br>- Tìm hiểu các lỗi 403 thường gặp khi lưu trữ website tĩnh | 28/09/2026 | 28/09/2026 | AWS Cloud Journey – Static Website Hosting with Amazon S3<br>AWS Docs – Hosting a static website using Amazon S3 |
| 2 | - Học module S3 Security Best Practices<br>- Tìm hiểu 4 tùy chọn S3 Block Public Access và cách AWS áp dụng mức hạn chế nghiêm ngặt nhất<br>- Phân biệt bucket policies, ACLs và Object Ownership (bucket owner enforced)<br>- Tìm hiểu mã hóa mặc định SSE-S3, versioning và access logging (CloudTrail data events)<br>- Kiểm tra cấu hình bằng lệnh aws s3api get-public-access-block | 29/09/2026 | 29/09/2026 | AWS Cloud Journey – S3 Security Best Practices<br>AWS Docs – Security best practices for Amazon S3<br>AWS Docs – Blocking public access to your Amazon S3 storage |
| 3 | - Học module Command Line Operations with AWS CLI<br>- Cài đặt AWS CLI và cấu hình profiles (aws configure / SSO)<br>- Thực hành các lệnh cho S3, EC2 và IAM với --query và --output<br>- Tìm hiểu cách lưu credentials an toàn trên máy cá nhân và không đưa vào repository | 30/09/2026 | 30/09/2026 | AWS Cloud Journey – Command Line Operations with AWS CLI<br>AWS Docs – AWS CLI User Guide |
| 4 | - Học module Monitoring with Amazon CloudWatch<br>- Xem metrics của EC2, tìm hiểu CloudWatch Logs và dashboards<br>- Tạo CPU alarm gửi thông báo qua Amazon SNS (email)<br>- Xác nhận đăng ký SNS và kiểm tra alarm hoạt động | 01/10/2026 | 01/10/2026 | AWS Cloud Journey – Monitoring with Amazon CloudWatch<br>AWS Docs – Amazon CloudWatch User Guide |
| 5 | - Học module Database Essentials with Amazon RDS<br>- Tìm hiểu Multi-AZ, automated backups và DB subnet groups<br>- Tạo RDS trong private subnet với Security Group chỉ cho phép truy cập từ application server<br>- Tìm hiểu mã hóa lúc lưu trữ (encryption at rest) và xóa tài nguyên sau khi thực hành để tránh phát sinh phí | 02/10/2026 | 02/10/2026 | AWS Cloud Journey – Database Essentials with Amazon RDS<br>AWS Docs – Amazon RDS User Guide |

### Kết quả đạt được trong Tuần 3:

- Lưu trữ được website tĩnh trên S3 và hiểu rằng bucket riêng tư không đồng nghĩa với việc mọi truy cập đều bị chặn.
- Nắm các lớp bảo vệ của S3: Block Public Access, bucket policies, encryption, versioning và logging.
- Sử dụng AWS CLI cơ bản với profiles và biết cách tránh lộ credentials.
- Tạo được CloudWatch alarm kèm thông báo qua SNS.
- Hiểu mô hình đặt database trong private subnet và kiểm soát truy cập bằng Security Groups.