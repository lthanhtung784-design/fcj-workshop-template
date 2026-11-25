---
title: "5.8 · Thu dọn tài nguyên"
weight: 8
chapter: false
aliases:
  - /vi/5-workshop/09-demo-cleanup/
---

1. Giữ môi trường hoạt động nếu giám khảo còn cần dùng đường dẫn. Xuất bằng chứng kiểm thử, estimate và số Billing. Ghi danh sách tài nguyên theo stack chính, stack KB và các tài nguyên tạo ngoài stack.
2. Khi đến thời điểm dọn, dừng nhận báo cáo mới, rà execution đang chờ duyệt và xử lý theo chính sách lab. Gỡ **riêng** receipt rule của lab. Nếu dùng DNS hoặc domain chung, bảo toàn MX và các rule phục vụ email khác.
3. Gỡ liên kết resource ở CloudFront khi phù hợp, disable distribution, đợi **Deployed** rồi xóa khi đã sẵn sàng. Kiểm tra subscription flat-rate, WAF/Web ACL và phí theo kỳ. Hủy đăng ký email demo nếu topic được giữ lại.
4. Xóa data source/KB trước các tài nguyên vector liên quan. Rà stack và tài nguyên có `Retain` hoặc `RetainExceptOnCreate`, gồm bảng, bucket, khóa, user pool. Với S3 versioned, kiểm tra cả version lẫn delete marker. Giữ evidence đến hết retention đã cam kết, rồi dọn bằng quy trình đã được nhóm cho phép.
5. Rà CloudFormation, S3, S3 Vectors, Bedrock Guardrail, IAM role, Cognito domain, CloudWatch logs/alarms, SQS, SNS, Route 53, Budgets và bucket artifact SAM nếu dành riêng cho lab. Chỉ lên lịch xóa KMS key sau khi xác định dữ liệu nào còn cần giải mã. Kiểm tra Bills/Cost Explorer lại sau khi số liệu cập nhật, gồm phí domain gia hạn tự động nếu mua riêng.

Với stack edge riêng, tháo association của ACL khỏi distribution trước khi xóa ACL và stack của nó. Ghi từng tài nguyên còn giữ, người phụ trách và ngày kiểm phí lần tiếp theo.
