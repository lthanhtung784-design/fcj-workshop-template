---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu Tuần 4:

- Hiểu cách truy cập riêng tư tới S3 thông qua VPC endpoints.
- Giám sát lưu lượng mạng bằng VPC Flow Logs.
- Quản trị EC2 mà không cần mở cổng SSH bằng Systems Manager Session Manager.
- Tổ chức tài nguyên bằng tags và kiểm soát quyền theo tag.

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Học module Private Access to S3 with VPC Endpoints<br>- Tìm hiểu gateway endpoints và cách route tables được cập nhật<br>- Cấu hình endpoint policy để giới hạn các bucket có thể truy cập<br>- Kiểm chứng EC2 trong private subnet truy cập được S3 mà không đi qua Internet | 05/10/2026 | 05/10/2026 | AWS Cloud Journey – Private Access to S3 with VPC Endpoints<br>AWS Docs – Gateway endpoints for Amazon S3 |
| 2 | - Học module Network Monitoring with VPC Flow Logs<br>- Bật Flow Logs và gửi log về CloudWatch Logs hoặc S3<br>- Đọc các bản ghi ACCEPT/REJECT và nhận diện lưu lượng dò quét cổng tự động (port-scanning)<br>- Liên hệ kết quả với việc siết chặt Security Groups và Network ACLs | 06/10/2026 | 06/10/2026 | AWS Cloud Journey – Network Monitoring with VPC Flow Logs<br>AWS Docs – Logging IP traffic using VPC Flow Logs |
| 3 | - Học module Systems Management with AWS Systems Manager<br>- Tìm hiểu các tính năng chính (Run Command, Patch Manager, Parameter Store)<br>- Gắn role AmazonSSMManagedInstanceCore cho EC2 để Systems Manager quản lý<br>- Ghi lại các điều kiện để instance xuất hiện trong Fleet Manager | 07/10/2026 | 07/10/2026 | AWS Cloud Journey – Systems Management with AWS Systems Manager<br>AWS Docs – AWS Systems Manager User Guide |
| 4 | - Học module Remote Server Access with Systems Manager Session Manager<br>- Kết nối tới EC2 mà không cần mở cổng 22 hoặc dùng key pair<br>- Tìm hiểu cách kiểm soát truy cập bằng IAM và cách ghi log phiên làm việc<br>- So sánh Session Manager với SSH truyền thống | 08/10/2026 | 08/10/2026 | AWS Cloud Journey – Remote Server Access with Systems Manager Session Manager<br>AWS Docs – AWS Systems Manager Session Manager |
| 5 | - Học module Resource Organization with Tags and Resource Groups<br>- Thiết kế quy ước đặt tag (Project, Owner, Environment) và gom nhóm tài nguyên bằng Resource Groups<br>- Học module Access Control with IAM and Resource Tags<br>- Thực hành policy có điều kiện dựa trên tag (attribute-based access control) | 09/10/2026 | 09/10/2026 | AWS Cloud Journey – Resource Organization with Tags and Resource Groups<br>AWS Cloud Journey – Access Control with IAM and Resource Tags<br>AWS Docs – Tagging AWS resources<br>AWS Docs – Controlling access to AWS resources using tags |

### Kết quả đạt được trong Tuần 4:

- Hiểu cách EC2 trong private subnet truy cập S3 qua gateway endpoint được giới hạn bởi endpoint policy.
- Đọc được Flow Logs để nhận diện lưu lượng bị từ chối (REJECT) và kết nối bất thường.
- Quản lý EC2 qua Session Manager mà không cần mở cổng SSH.
- Thiết kế quy ước tag và áp dụng tag cho kiểm soát truy cập.
- Hiểu mối liên hệ giữa giám sát mạng, thu hẹp bề mặt tấn công và quản trị tập trung.