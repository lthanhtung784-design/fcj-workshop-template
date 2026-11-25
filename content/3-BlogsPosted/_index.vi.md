---
title: "Blogs Posted"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---



Phần này liệt kê và giới thiệu các bài blog đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj), tập trung vào cơ chế bảo mật AWS, nguyên tắc least privilege, bảo vệ dữ liệu và ứng phó sự cố.

### [Blog 1 - SQS FIFO CÓ THỰC SỰ ĐẢM BẢO “XỬ LÝ ĐÚNG MỘT LẦN” (EXACTLY-ONCE PROCESSING)?](3.1-Blog1/)
Bài viết làm rõ lý do xử lý trùng lặp vẫn có thể xảy ra trên hàng đợi Amazon SQS FIFO—chẳng hạn khi hàm Lambda ghi vào DynamoDB thành công nhưng bị timeout trước khi xóa message—bằng cách phân biệt cơ chế chống trùng lặp ở tầng queue (cửa sổ 5 phút, SHA-256 chỉ tính trên message body) với hiệu ứng nghiệp vụ đầu-cuối, đồng thời trình bày cơ chế retry at-least-once của Lambda, idempotency (`ConditionExpression` trên `PutItem`), tác vụ phụ bên ngoài, `ReportBatchItemFailures` trên hàng đợi FIFO, lưu ý khi redrive từ FIFO DLQ và 4 câu hỏi thiết kế hệ thống bất đồng bộ cốt lõi.

### [Blog 2 - AWS KMS & ENVELOPE ENCRYPTION: MÃ HÓA DỮ LIỆU ĐÃ ĐỦ AN TOÀN CHƯA?](3.2-Blog2/)
Bài viết phân tích cơ chế envelope encryption trên S3 SSE-KMS (`GenerateDataKey`, data key và KMS key), lý do mã hóa dữ liệu lưu trữ không thay thế phân quyền, vai trò của encryption context (AAD không bí mật), và tác động của S3 Bucket Keys khi giảm chi phí gọi KMS (tới 99%) nhưng đổi mặc định `aws:s3:arn` từ object ARN sang bucket ARN cũng như ảnh hưởng đến việc đánh giá KMS key policy và độ chi tiết CloudTrail.

### [Blog 3 - S3 ĐÃ BẬT BLOCK PUBLIC ACCESS THÌ DỮ LIỆU ĐÃ AN TOÀN CHƯA?](3.3-Blog3/)
Bài viết giải thích vì sao bật S3 Block Public Access không ngăn được việc truy cập bằng credentials hợp lệ bị lộ, đồng thời phân tích bảo vệ S3 theo 3 lớp: Prevention (4 tùy chọn Block Public Access, least privilege, Bucket owner enforced, mã hóa mặc định SSE-S3), Auditing (CloudTrail S3 Data Events) và Detection & Alerting (GuardDuty S3 Protection kết hợp EventBridge và SNS).

### [Blog 4 - MỘT QUYỀN IAM NHỎ CÓ THỂ GÂY RA RỦI RO LỚN NHƯ THẾ NÀO?](3.4-Blog4/)
Bài viết phân tích mức độ ảnh hưởng khi tài khoản IAM mang quyền `AdministratorAccess` bị chiếm quyền—từ rò rỉ/xóa dữ liệu S3, lạm dụng EC2 (như cryptojacking), phá hoại RDS, chiếm quyền/duy trì truy cập qua IAM đến can thiệp CloudTrail—cùng các biện pháp giảm thiểu như least privilege, MFA, temporary credentials qua IAM role, permission boundaries, giám sát CloudTrail và rà soát quyền định kỳ.

### [Blog 5 - AWS ACCESS KEY BỊ LỘ TRÊN GITHUB: AWS ĐÃ TỰ ĐỘNG QUARANTINE, VẬY CHÚNG TA CÒN PHẢI LÀM GÌ?](3.5-Blog5/)
Bài viết làm rõ cơ chế tự động của AWS khi phát hiện access key lộ trên GitHub (gắn quarantine policy như `AWSCompromisedKeyQuarantineV3` hoặc `AWSCompromisedKeyQuarantineV4` và thông báo qua AWS Health hoặc Support Case), trình bày quy trình xử lý 5 bước và các biện pháp phòng ngừa như IAM role, IAM Identity Center, GitHub Actions OIDC, Secret Scanning kèm Push Protection và `git-secrets`.