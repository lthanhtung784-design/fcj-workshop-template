---
title: "5.6 · Đánh giá Well-Architected"
weight: 6
chapter: false
---

Chọn một incident demo rồi mở đồng thời trang chi tiết, execution của Step Functions và phiên bản raw trong S3 bằng đúng quyền. Ba màn hình trả lời ba câu hỏi khác nhau: chuyên viên thấy gì, workflow đã đi qua đâu và hệ thống dùng bản gốc nào. Ghi thời điểm, mã sự cố và mã phiên bản vào phiếu kiểm thử. Đối chiếu dưới đây dùng cùng các hiện vật đó để xem xét thiết kế theo AWS Well-Architected.

| Tiêu chí | Quyết định trong PhishGuard | Cách kiểm tra và giới hạn của kết luận |
|---|---|---|
| Sơ đồ và triển khai (0,5) | CloudFront có WAF, đường web và SES hội tụ ở Ingest, raw được lưu trước khi mở workflow. Step Functions giữ callback chờ người duyệt. | Đối chiếu Behaviors, receipt rule, template và một execution với từng mũi tên ở 5.1. Lambda dùng mạng do AWS quản lý. SAM không khai báo subnet ứng dụng. |
| Operational Excellence (0,5) | Change set cho phép xem trước cập nhật. Hai alarm báo workflow lỗi và có dữ liệu trong DLQ qua SNS. | Ở 5.5.1, kiểm tra cả trạng thái, Actions và ARN đích. Khi nhận cảnh báo, tìm thời điểm và execution hoặc log Ingest tương ứng. Ảnh alarm OK chỉ ghi trạng thái lúc chụp. |
| Security (0,5) | JWT và quyền theo vai trò kiểm soát API. S3 giữ raw riêng, có SSE-KMS, versioning và Object Lock Governance 7 ngày. Người phê duyệt dùng Admin API. | Chạy H02 và H15 với hai reporter và auditor. So GET có header với GET thường ở bước WAF. Khi trình duyệt POST file thẳng đến S3, chính sách ký và Ingest kiểm soát đường này. Quyền bypass Governance cần giới hạn. |
| Reliability (0,5) | Ingest dùng định danh yêu cầu để xử lý lần gửi lại. Sau khi retry bất đồng bộ hết lượt, lỗi được chuyển vào DLQ. Workflow có nhánh timeout và tổng hợp có fallback. | Chạy H01/H04 và H13/H14 trong môi trường demo. Nếu DLQ có bản tin, xác định nguyên nhân, kiểm incident và phiên bản raw trước khi cho xử lý lại. Triển khai một Region. RTO và RPO sau sự cố toàn vùng chưa được đo. |
| Performance Efficiency (0,5) | Upload trực tiếp giảm dữ liệu chuyển qua API. Ảnh dùng Lambda x86_64 512 MiB với OCR/QR. Người duyệt có thể phản hồi sau khi Lambda chuẩn bị đã kết thúc. | So Duration p50/p95, Billed Duration, Max Memory Used của nhóm ảnh và văn bản có kích thước biết trước. Kiểm Throttles và thời gian chờ phê duyệt riêng. Workshop chưa công bố kết quả benchmark. |
| Cost Optimization (0,5) | Mô hình theo số báo cáo, số ảnh, lượt gọi AI và phí dịch vụ cố định. WAF là dòng lớn nhất của kịch bản 300 báo cáo/tháng. | Tái tính từ CSV ở 5.7, đổi một giả định, rồi đối chiếu báo cáo Billing đúng kỳ. Ghi rõ các phần phí chia sẻ như hosted zone và các khoản có thể tiếp tục sau lab. |
| Sustainability (ghi nhận, 0 điểm) | Xử lý theo sự kiện, vòng đời cho intake và giới hạn thời gian lưu dữ liệu tạm. | Kiểm lifecycle và phiên bản cũ sau thử nghiệm. Chỉ xóa sau khi phân biệt dữ liệu tạm với bằng chứng còn retention. Chưa có số đo phát thải cho workload này. |

### Khi cần xử lý một cảnh báo

Nếu alarm DLQ báo có bản tin, lưu timestamp và request ID. Tìm lần gọi bất đồng bộ của Ingest trong CloudWatch Logs, kiểm object nguồn còn truy cập được và quyền đọc/ghi cần thiết. Đối chiếu DynamoDB, raw version và execution theo incident trước khi thử lại bằng dữ liệu lab. Một lần thử khôi phục đạt khi số incident và execution đúng kỳ vọng, bản gốc vẫn tra được và lần lỗi đầu tiên còn có thể giải thích qua log.

### Điều cần tự giải thích khi bảo vệ

Chọn một mũi tên người nghe dễ hiểu nhầm, chẳng hạn đường upload trực tiếp hay callback. Mở cấu hình thật, trình bày bên gọi, bên nhận, dữ liệu đi qua và một tình huống lỗi. Với hình kiến trúc có AI hỗ trợ, mô tả đúng phần việc thực tế của mình và giữ lịch sử chỉnh sửa nếu có. Một mục tiêu thiết kế hoặc dự toán đều cần được ghi đúng loại minh chứng.

[Khung AWS Well-Architected](https://docs.aws.amazon.com/wellarchitected/latest/framework/the-pillars-of-the-framework.html) · [Barem workshop FCAJ](https://hcm-rules.awsfcaj.com/scoring/workshop)
