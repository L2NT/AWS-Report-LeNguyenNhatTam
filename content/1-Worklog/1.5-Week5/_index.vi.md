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
* Tích hợp bước kiểm thử tự động (pytest) vào CodePipeline.
* Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund".

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Thiết lập các CloudWatch Alarms giám sát hệ thống kèm SNS Topic gửi cảnh báo qua email <br>&emsp;+ Theo dõi các chỉ số quan trọng của Lambda (số lỗi, thời gian xử lý, số lần bị giới hạn) và của API Gateway (lỗi 5xx), đặt ngưỡng cảnh báo phù hợp cho từng chỉ số <br>&emsp;+ Tạo SNS Topic, đăng ký email nhận cảnh báo và xác nhận đăng ký | 20/07/2026 | 20/07/2026 | [Using Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| 3 | - Bật S3 Intelligent-Tiering cho bucket lưu tài liệu người dùng để tự động tối ưu chi phí <br>&emsp;+ Cấu hình lifecycle rule tự động chuyển các đối tượng sang lớp lưu trữ thông minh ngay khi tải lên, giúp giảm chi phí cho tài liệu ít được truy cập | 21/07/2026 | 21/07/2026 | [Managing storage costs with S3 Intelligent-Tiering](https://docs.aws.amazon.com/AmazonS3/latest/userguide/intelligent-tiering.html) |
| 4 | - Bổ sung cơ chế chống tấn công CSRF cho luồng đăng nhập Google: sinh một mã xác thực ngẫu nhiên cho mỗi lần đăng nhập, đối chiếu lại khi Cognito chuyển hướng về <br>&emsp;+ Nhận diện lỗ hổng trước khi khắc phục: luồng đăng nhập Google thiếu tham số xác thực ngẫu nhiên, kẻ tấn công có thể dụ nạn nhân đăng nhập vào tài khoản do kẻ tấn công kiểm soát <br>&emsp;+ Đối chiếu mã xác thực trả về với mã đã lưu, xóa ngay sau khi dùng để chống tấn công phát lại (replay attack) | 22/07/2026 | 22/07/2026 | [CSRF Prevention Cheat Sheet – OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) |
| 5 | - Kiểm thử đầy đủ 5 kịch bản CSRF (đăng nhập bình thường, mã xác thực đúng định dạng, giả lập tấn công bị chặn ở tầng ứng dụng, mã đúng nhưng code giả bị Cognito chặn, mã bị xóa sau khi dùng) <br>&emsp;+ Giả lập tấn công thật: nhập tay đường dẫn callback với mã xác thực không khớp — xác nhận bị chặn ngay ở tầng ứng dụng trước khi gọi tới Cognito <br>&emsp;+ Kiểm thử riêng trường hợp mã xác thực đúng nhưng code giả — xác nhận Cognito tự chặn ở tầng thứ hai, chứng minh hệ thống có 2 lớp bảo vệ độc lập <br> - Bật mã hóa KMS cho DynamoDB <br>&emsp;+ So sánh giữa AWS owned key (miễn phí, mặc định) và AWS managed key (có nhật ký truy vết qua CloudTrail) — chọn managed key vì cần theo dõi truy cập nhưng không cần quản lý khóa thủ công | 23/07/2026 | 23/07/2026 | [DynamoDB encryption at rest](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/EncryptionAtRest.html) |
| 6 | - Tích hợp bước kiểm thử tự động (pytest) vào quy trình CI/CD trên CodePipeline: kiểm tra định dạng mã nguồn và chạy bộ kiểm thử trước mỗi lần build/deploy <br>&emsp;+ Cân nhắc đặt bước kiểm thử ở giai đoạn đầu để quy trình dừng sớm nếu kiểm thử thất bại, tránh tốn thời gian build Docker image không cần thiết <br>&emsp;+ Cấu hình bước kiểm tra định dạng chỉ cảnh báo (không chặn build), nhưng bộ kiểm thử đơn vị sẽ chặn build thật sự nếu thất bại | 24/07/2026 | 24/07/2026 | [Build specification reference – CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html) |
| 7   | - **Họp nhóm:** Rà soát tiến độ công việc, đọc và sửa lỗi báo cáo giữa các thành viên trong nhóm <br>&emsp;+ Đọc chéo báo cáo của các thành viên, góp ý lỗi chính tả/nội dung chưa nhất quán <br> - Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund" | 25/07/2026 | 25/07/2026 | |


### Kết quả đạt được tuần 5:

* Triển khai 4 CloudWatch Alarms + SNS để chủ động phát hiện lỗi/hiệu năng bất thường thay vì chờ người dùng phản ánh.
* Bật S3 Intelligent-Tiering giúp tối ưu chi phí lưu trữ tài liệu người dùng.
* Bổ sung cơ chế chống tấn công CSRF 2 lớp cho luồng đăng nhập Google, đã kiểm thử đầy đủ 5 kịch bản kể cả giả lập tấn công.
* Bật mã hóa KMS cho bảng DynamoDB chứa hồ sơ người dùng, có đầy đủ nhật ký truy vết qua CloudTrail.
* Tích hợp bước kiểm thử tự động (pytest) vào quy trình CI/CD - một lớp bảo đảm chất lượng mới trước khi build và triển khai.
* Họp nhóm, rà soát tiến độ và phối hợp chỉnh sửa lỗi trong báo cáo giữa các thành viên.
* Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund" (25/07/2026) - xem chi tiết tại mục 4.2.


