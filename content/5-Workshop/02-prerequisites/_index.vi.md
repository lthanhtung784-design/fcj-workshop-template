---
title: "Chuẩn bị môi trường"
weight: 2
chapter: false
---

Dùng một tài khoản lab mà người triển khai được phép quản lý, chọn **US East (N. Virginia), us-east-1**. Tên vật lý của một số Lambda, bảng, user pool group và IAM role được cố định trong mẫu. Khi học lại trên tài khoản đã có PhishGuard, bắt đầu từ phần đối chiếu của stack hiện tại. Để dựng độc lập từ đầu, dùng một tài khoản lab riêng.

- Cài Git, Python 3.12 x64, Node.js 22 LTS, AWS CLI v2 và AWS SAM CLI. Docker chỉ cần cho phương án build trong container Linux. Người triển khai cần quyền quản lý stack, đóng gói S3 và triển khai các tài nguyên trong template, gồm quyền chuyển đúng role cho dịch vụ. Người phụ trách Billing cần đọc Bills, Cost Explorer và quản lý Budgets.
- Chuẩn bị quyền chỉnh DNS trên một domain hoặc subdomain nhận thư. Dùng ba địa chỉ kiểm thử do nhóm sở hữu, riêng cho reporter, admin, auditor; thêm một tài khoản reporter thứ hai để kiểm thử phân tách người dùng.
- Cấu hình profile AWS tên `phishguard` bằng cơ chế đăng nhập của tài khoản. Profile này chọn danh tính AWS của người triển khai. Các tài khoản `demo-*` đăng nhập ứng dụng bằng Cognito.
- Giải nén [PhishGuard-Lab.zip](/downloads/PhishGuard-Lab.zip). Thư mục `lab/` chứa mã thực hành, `tools/` chứa công cụ đọc cấu hình. Các đoạn PowerShell phía dưới dùng chung một cửa sổ terminal trong `lab/`.

```powershell
Set-Location .\lab
$pgProfile = 'phishguard'
$pgRegion = 'us-east-1'
$pgStack = 'phishguard-ai'
aws sts get-caller-identity --profile $pgProfile --query '{Account:Account,Arn:Arn}'
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements-dev.txt
.\.venv\Scripts\python.exe -m pip install "moto[s3,dynamodb]==5.2.5"
sam --version
node --version
Test-Path .\layers\ocr-vie-py312-x86_64.zip
```

**Mốc kiểm tra.** Account phải là tài khoản lab được chọn, Python là 3.12, `Test-Path` trả `True`. Nếu profile dùng IAM Identity Center và phiên đã hết hạn, chạy `aws sso login --profile phishguard`.

