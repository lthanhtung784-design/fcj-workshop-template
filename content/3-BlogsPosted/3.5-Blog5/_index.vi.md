---
title: "Blog 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 3.5. </b> "
---


# AWS ACCESS KEY BỊ LỘ TRÊN GITHUB: AWS ĐÃ TỰ ĐỘNG QUARANTINE, VẬY CHÚNG TA CÒN PHẢI LÀM GÌ?

Khi tìm hiểu về sự cố lộ AWS Access Key, nhiều người dễ nghĩ rằng có cơ chế tự động phát hiện và xử lý từ AWS thì rủi ro không quá đáng lo. Thực tế, AWS hỗ trợ phát hiện và giảm thiểu thiệt hại, nhưng quarantine tự động không đồng nghĩa tài khoản đã an toàn hay việc xử lý sự cố đã hoàn tất. Bài viết tóm tắt cách AWS phản ứng khi phát hiện key bị lộ, quy trình xử lý 5 bước và các biện pháp phòng ngừa cho project cá nhân và nhóm.

Key points to remember:

- **AWS tự động làm gì:** AWS có thể phát hiện credential lộ trên các nguồn như GitHub, gắn quarantine policy (như `AWSCompromisedKeyQuarantineV3` hoặc `AWSCompromisedKeyQuarantineV4`) cho IAM identity liên quan và gửi thông báo qua AWS Health hoặc Support Case (một thử nghiệm của Unit 42 ghi nhận gắn policy V3 sau khoảng 10 giây, nhưng đây không phải thời gian đảm bảo cho mọi trường hợp). Quarantine policy thêm các `Deny` cho một số hành động cụ thể chứ không vô hiệu hóa hoàn toàn key, nên các hành động ngoài phạm vi bị chặn vẫn phụ thuộc vào quyền IAM khác của identity đó.
- **Quy trình xử lý 5 bước:** (1) Cô lập key bằng cách xác định IAM user, đánh giá quyền và chuyển key sang `Inactive` (chưa cần xóa ngay nếu cần đối chiếu vận hành); (2) khôi phục quyền truy cập hợp lệ cho workload và chuyển sang IAM role/temporary credentials thay vì key dài hạn; (3) điều tra trên AWS CloudTrail (API, thời điểm, IP nguồn, Region và thay đổi IAM/tài nguyên) bằng một principal quản trị độc lập và lưu ý phạm vi log như S3 data events; (4) kiểm tra dấu hiệu xâm nhập toàn tài khoản (IAM user/role/policy mới hoặc bị sửa, EC2/Lambda/S3 bất thường, Region lạ và chi phí trên Billing); và (5) hoàn tất khắc phục theo hướng dẫn trong AWS Support Case, không tự ý gỡ quarantine policy chỉ vì hệ thống chạy lại được.
- **Ưu tiên phòng ngừa:** Dùng IAM role cho workload trên AWS, IAM Identity Center/federation thay cho access key dài hạn của người dùng, GitHub Actions OIDC thay vì lưu secret dài hạn, bật GitHub Secret Scanning kèm Push Protection và dùng `git-secrets` ở máy local—đồng thời nhớ rằng xóa file hay commit không giúp credential an toàn nếu đã từng lộ ra ngoài.
![Blog 5 screenshot](/images/3-BlogsPosted/3.5-Blog4/blog5.png)
https://www.facebook.com/groups/awsstudygroupfcj/permalink/2346834029414889/