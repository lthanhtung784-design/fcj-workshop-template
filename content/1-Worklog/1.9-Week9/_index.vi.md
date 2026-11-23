---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu Tuần 9:

- Hiểu các thực hành bảo mật cơ bản với Docker và Amazon ECS.
- Xây dựng pipeline CI/CD với CodePipeline mà không lưu key trong repository.
- Hiểu cơ chế gửi nhận bất đồng bộ với SQS và SNS.
- Giám sát ứng dụng serverless với X-Ray và CloudWatch.

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Học module Containerization with Docker<br>- Viết Dockerfile, build và chạy container<br>- Tìm hiểu thực hành an toàn: image gọn nhẹ, không chạy quyền root, không nhúng secrets vào image<br>- Tìm hiểu quét lỗ hổng image (image vulnerability scanning) | 09/11/2026 | 09/11/2026 | AWS Cloud Journey – Containerization with Docker<br>Docker Docs – Dockerfile best practices |
| 2 | - Học module Container Orchestration with Amazon ECS<br>- Tạo cluster, task definition và service với Fargate<br>- Phân biệt task role và task execution role<br>- Nạp secrets từ Secrets Manager vào container thay vì hard-code biến môi trường | 10/11/2026 | 10/11/2026 | AWS Cloud Journey – Container Orchestration with Amazon ECS<br>AWS Docs – Amazon ECS Developer Guide |
| 3 | - Học module CI/CD Pipeline with AWS CodePipeline<br>- Xây dựng pipeline gồm các giai đoạn source, build và deploy<br>- Hiểu IAM service role và artifact store của pipeline<br>- Xác nhận không lưu access keys trong mã nguồn hoặc file cấu hình, liên kết với bài học lộ key | 11/11/2026 | 11/11/2026 | AWS Cloud Journey – CI/CD Pipeline with AWS CodePipeline<br>AWS Docs – AWS CodePipeline User Guide<br>AWS Labs – git-secrets (<https://github.com/awslabs/git-secrets>) |
| 4 | - Học module Messaging Systems with SQS and SNS<br>- Phân biệt queues và topics, thử nghiệm publish/subscribe<br>- Cấu hình dead-letter queue và server-side encryption<br>- Tìm hiểu access policies cho queue/topic để ngăn truy cập ngoài ý muốn | 12/11/2026 | 12/11/2026 | AWS Cloud Journey – Messaging Systems with SQS and SNS<br>AWS Docs – Amazon SQS Developer Guide<br>AWS Docs – Amazon SNS Developer Guide |
| 5 | - Học module Distributed Tracing with X-Ray and CloudWatch<br>- Bật tracing cho Lambda/API và đọc service map<br>- Tạo CloudWatch alarms cho lỗi (errors) và độ trễ (latency)<br>- Tóm tắt cách kết hợp logs, metrics và traces khi điều tra sự cố | 13/11/2026 | 13/11/2026 | AWS Cloud Journey – Distributed Tracing with X-Ray and CloudWatch<br>AWS Docs – AWS X-Ray Developer Guide |

### Kết quả đạt được trong Tuần 9:

- Nắm được các thực hành an toàn khi đóng gói và chạy container.
- Phân biệt được task role và execution role trong ECS, lấy secrets đúng cách.
- Xây dựng được pipeline CI/CD mà không làm lộ credentials trong repository.
- Hiểu cách tách rời hệ thống bằng SQS/SNS và bảo vệ bằng policies, mã hóa.
- Biết kết hợp logs, metrics và traces khi điều tra sự cố.