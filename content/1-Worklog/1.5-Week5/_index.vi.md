---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
### Mục tiêu tuần 5:

* Tăng cường giám sát hệ thống bằng CloudWatch Alarms.
* Tối ưu chi phí lưu trữ S3 và siết bảo mật (KMS cho DynamoDB, CSRF cho đăng nhập Google).
* Thêm bước kiểm thử tự động (pytest) vào CodePipeline.
* Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund".

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Thiết lập 4 CloudWatch Alarms (lambda-errors, lambda-duration, lambda-throttles, apigateway-5xx) + SNS Topic gửi cảnh báo qua email <br>&emsp;+ Chọn ngưỡng cụ thể cho từng alarm: lambda-errors > 5 lỗi/5 phút, lambda-duration > 25000ms/5 phút (gần chạm timeout 30s), lambda-throttles ≥ 1 lần/5 phút, apigateway-5xx > 5 lỗi/5 phút <br>&emsp;+ Tạo SNS Topic, đăng ký email nhận cảnh báo, xác nhận subscription qua link trong email | 20/07/2026 | 20/07/2026 | [Using Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| 3 | - Bật S3 Intelligent-Tiering cho bucket lưu file người dùng để tự động tối ưu chi phí <br>&emsp;+ Tạo lifecycle rule transition mọi object sang `INTELLIGENT_TIERING` ngay khi upload (0 ngày) <br>&emsp;+ Lưu ý AWS chỉ áp dụng transition cho object ≥ 128KB — phù hợp với tài liệu PDF/DOCX của dự án vốn thường lớn hơn ngưỡng này | 21/07/2026 | 21/07/2026 | [Managing storage costs with S3 Intelligent-Tiering](https://docs.aws.amazon.com/AmazonS3/latest/userguide/intelligent-tiering.html) |
| 4 | - Lên văn phòng. Thêm CSRF protection cho luồng đăng nhập Google: sinh `state = crypto.randomUUID()` lưu ở `sessionStorage`, xác minh bằng `verifyOAuthState()` khi callback <br>&emsp;+ Nhận diện lỗ hổng trước khi sửa: luồng Google Login qua Cognito Hosted UI không có tham số `state`, kẻ tấn công có thể dụ nạn nhân click link chứa authorization code dựng sẵn (Login CSRF/OAuth code injection) <br>&emsp;+ Thêm `verifyOAuthState()` so sánh state trả về với state đã lưu, xóa ngay sau khi dùng để chống replay attack | 22/07/2026 | 22/07/2026 | [CSRF Prevention Cheat Sheet – OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) |
| 5 | - Test 5 kịch bản CSRF (đăng nhập bình thường, state đúng định dạng, giả lập tấn công CSRF bị chặn ở tầng app, state đúng nhưng code giả bị Cognito chặn, state bị xóa sau khi dùng) <br>&emsp;+ Giả lập tấn công thật: copy `state` hợp lệ từ sessionStorage, gõ tay URL callback với `state` khác — xác nhận bị chặn ngay ở tầng app trước khi gọi tới Cognito <br>&emsp;+ Test riêng trường hợp `state` đúng nhưng `code` giả — xác nhận Cognito tự chặn ở tầng thứ 2 (invalid_grant), chứng minh hệ thống có 2 lớp bảo vệ độc lập <br> - Bật mã hóa KMS cho DynamoDB (đổi từ AWS owned key sang `alias/aws/dynamodb`) <br>&emsp;+ So sánh AWS owned key (miễn phí, mặc định) với AWS managed key (`alias/aws/dynamodb`, có audit trail qua CloudTrail) — chọn managed key vì cần theo dõi truy cập nhưng không cần quản lý key thủ công như customer managed key | 23/07/2026 | 23/07/2026 | [DynamoDB encryption at rest](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/EncryptionAtRest.html) |
| 6 | - Thêm bước pytest vào `pre_build` của CodePipeline (`backend/buildspec.yml`): chạy `flake8` lint + `pytest test_*_unit.py` trước mỗi lần build/deploy <br>&emsp;+ Cân nhắc đặt bước test ở `pre_build` thay vì `build`/`post_build` để build/deploy dừng sớm nếu test fail, tránh tốn thời gian build Docker image không cần thiết <br>&emsp;+ Cấu hình `flake8` chạy với `--exit-zero` (không chặn build vì lint) nhưng `pytest` chặn build thật sự nếu unit test fail | 24/07/2026 | 24/07/2026 | [Build specification reference – CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html) |
| 7   | - Họp nhóm: Review tiến độ công việc, đọc và sửa lỗi báo cáo giữa các thành viên trong nhóm <br>&emsp;+ Đọc chéo report của Trọng và Phong, góp ý lỗi chính tả/nội dung chưa nhất quán <br> - Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund" | 25/07/2026 | 25/07/2026 | |


### Kết quả đạt được tuần 5:

* Triển khai 4 CloudWatch Alarms + SNS để chủ động phát hiện lỗi/hiệu năng bất thường thay vì chờ user report.
* Bật S3 Intelligent-Tiering giúp tối ưu chi phí lưu trữ tài liệu người dùng.
* Thêm CSRF protection 2 lớp cho luồng đăng nhập Google, đã test đầy đủ 5 kịch bản kể cả giả lập tấn công.
* Bật mã hóa KMS cho bảng DynamoDB chứa profile người dùng, có đầy đủ audit trail qua CloudTrail.
* Thêm bước pytest chạy trong CodePipeline (`pre_build`) - một lớp bảo mật/chất lượng mới trước khi build & deploy.
* Họp nhóm, review tiến độ và phối hợp chỉnh sửa lỗi trong báo cáo giữa các thành viên.
* Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund" (25/07/2026) - xem chi tiết tại mục 4.2.


