---
title: "Nhật ký Tuần 5: Tăng cường giám sát, tối ưu chi phí & Củng cố bảo mật"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
### Mục tiêu tuần 5:

* Tăng cường giám sát hệ thống bằng CloudWatch Alarms.
* Tối ưu chi phí lưu trữ S3 và củng cố bảo mật (mã hóa KMS cho DynamoDB, chống CSRF cho đăng nhập Google).
* Tích hợp bước test tự động (pytest) vào CodePipeline.
* Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund".

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Thiết lập CloudWatch Alarms giám sát hệ thống kèm SNS Topic gửi cảnh báo qua email <br>&emsp;+ Theo dõi các chỉ số quan trọng của Lambda (số lỗi, thời gian xử lý, số lần bị giới hạn) và API Gateway (lỗi 5xx), đặt ngưỡng phù hợp cho từng chỉ số <br>&emsp;+ Tạo SNS Topic, đăng ký và xác nhận email nhận cảnh báo | 20/07/2026 | 20/07/2026 | [Using Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| 3 | - Bật S3 Intelligent-Tiering cho bucket lưu tài liệu để tự động tối ưu chi phí: cấu hình lifecycle rule chuyển đối tượng sang lớp lưu trữ thông minh ngay khi tải lên, giảm chi phí cho tài liệu ít truy cập | 21/07/2026 | 21/07/2026 | [Managing storage costs with S3 Intelligent-Tiering](https://docs.aws.amazon.com/AmazonS3/latest/userguide/intelligent-tiering.html) |
| 4 | - Bổ sung cơ chế chống CSRF cho flow đăng nhập Google: sinh mã xác thực ngẫu nhiên mỗi lần đăng nhập, đối chiếu lại khi Cognito redirect về, không khớp thì chặn; mã dùng xong xóa ngay để tránh tái sử dụng | 22/07/2026 | 22/07/2026 | [CSRF Prevention Cheat Sheet – OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) |
| 5 | - Test 5 kịch bản CSRF (đăng nhập bình thường, mã đúng định dạng, mock tấn công bị chặn ở tầng ứng dụng, mã đúng nhưng code giả bị Cognito chặn, mã bị xóa sau khi dùng) <br>&emsp;+ Mock tấn công thật: nhập tay callback với mã không khớp — xác nhận bị chặn ngay ở tầng ứng dụng trước khi gọi Cognito <br>&emsp;+ Trường hợp mã đúng nhưng code giả: Cognito tự chặn ở tầng thứ hai, chứng minh hệ thống có 2 lớp bảo vệ độc lập <br> - Bật mã hóa KMS cho DynamoDB: so sánh AWS owned key (miễn phí, mặc định) và AWS managed key (có nhật ký CloudTrail) — chọn managed key vì cần theo dõi truy cập mà không phải quản lý khóa thủ công | 23/07/2026 | 23/07/2026 | [DynamoDB encryption at rest](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/EncryptionAtRest.html) |
| 6 | - Tích hợp bước test tự động (pytest) vào CI/CD trên CodePipeline: kiểm tra định dạng mã và chạy bộ test trước mỗi lần build/deploy <br>&emsp;+ Đặt bước test ở giai đoạn đầu để dừng sớm nếu thất bại, tránh tốn thời gian build Docker image <br>&emsp;+ Bước kiểm tra định dạng chỉ cảnh báo, riêng bộ test đơn vị sẽ chặn build nếu thất bại | 24/07/2026 | 24/07/2026 | [Build specification reference – CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html) |
| 7   | - Họp nhóm: Rà soát tiến độ, đọc chéo và sửa lỗi báo cáo giữa các thành viên (góp ý lỗi chính tả/nội dung chưa nhất quán) <br> - Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund" | 25/07/2026 | 25/07/2026 | |


### Kết quả đạt được tuần 5:

* Triển khai 4 CloudWatch Alarms + SNS để chủ động phát hiện lỗi/hiệu năng bất thường thay vì chờ người dùng phản ánh.
* Bật S3 Intelligent-Tiering để tối ưu chi phí lưu trữ tài liệu.
* Bổ sung cơ chế chống CSRF 2 lớp cho flow đăng nhập Google, đã test 5 kịch bản gồm mock tấn công.
* Bật mã hóa KMS cho bảng DynamoDB chứa profile người dùng, có nhật ký truy vết qua CloudTrail.
* Tích hợp bước test tự động (pytest) vào CI/CD - một lớp bảo đảm chất lượng mới trước khi build và triển khai.
* Họp nhóm, rà soát tiến độ và phối hợp chỉnh sửa lỗi báo cáo giữa các thành viên.
* Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund" (25/07/2026) - xem chi tiết tại mục 4.2.


