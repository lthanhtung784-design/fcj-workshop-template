---
title: "5.3 · Triển khai ứng dụng"
weight: 3
chapter: false
---

Dựng backend trước để lấy Outputs cho portal. Khi đã có ID distribution, mới gắn Web ACL và kiểm tra tại biên.

| Mục | Kết quả cần có |
|---|---|
| [5.3.1 · Backend và xử lý ảnh](backend/) | Dựng stack SAM và kiểm hai layer xử lý ảnh. |
| [5.3.2 · Portal và phân quyền](portal/) | Cấu hình Cognito, hai origin CloudFront và frontend dùng API thật. |
| [5.3.3 · Bảo vệ CloudFront bằng WAF](waf/) | Gắn ACL, chứng minh luật header chặn được và thử lại portal. |
