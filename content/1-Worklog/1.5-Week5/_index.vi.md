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
| 2 | - Thiết lập 4 CloudWatch Alarms (lambda-errors, lambda-duration, lambda-throttles, apigateway-5xx) + SNS Topic gửi cảnh báo qua email | 20/07/2026 | 20/07/2026 | |
| 3 | - Bật S3 Intelligent-Tiering cho bucket lưu file người dùng để tự động tối ưu chi phí | 21/07/2026 | 21/07/2026 | |
| 4 | - Thêm CSRF protection cho luồng đăng nhập Google: sinh `state = crypto.randomUUID()` lưu ở `sessionStorage`, xác minh bằng `verifyOAuthState()` khi callback | 22/07/2026 | 22/07/2026 | |
| 5 | - Test 5 kịch bản CSRF (đăng nhập bình thường, state đúng định dạng, giả lập tấn công CSRF bị chặn ở tầng app, state đúng nhưng code giả bị Cognito chặn, state bị xóa sau khi dùng) <br> - Bật mã hóa KMS cho DynamoDB (đổi từ AWS owned key sang `alias/aws/dynamodb`) | 23/07/2026 | 23/07/2026 | |
| 6 | - Thêm bước pytest vào `pre_build` của CodePipeline (`backend/buildspec.yml`): chạy `flake8` lint + `pytest test_*_unit.py` trước mỗi lần build/deploy | 24/07/2026 | 24/07/2026 | |
| 7   | - Họp nhóm: Review tiến độ công việc, đọc và sửa lỗi báo cáo giữa các thành viên trong nhóm <br> - Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund" | 25/07/2026 | 25/07/2026 | |


### Kết quả đạt được tuần 5:

* Triển khai 4 CloudWatch Alarms + SNS để chủ động phát hiện lỗi/hiệu năng bất thường thay vì chờ user report.
* Bật S3 Intelligent-Tiering giúp tối ưu chi phí lưu trữ tài liệu người dùng.
* Thêm CSRF protection 2 lớp cho luồng đăng nhập Google, đã test đầy đủ 5 kịch bản kể cả giả lập tấn công.
* Bật mã hóa KMS cho bảng DynamoDB chứa profile người dùng, có đầy đủ audit trail qua CloudTrail.
* Thêm bước pytest chạy trong CodePipeline (`pre_build`) - một lớp bảo mật/chất lượng mới trước khi build & deploy.
* Họp nhóm, review tiến độ và phối hợp chỉnh sửa lỗi trong báo cáo giữa các thành viên.
* Tham gia hackathon "FCAJ x Agentic AI Build Week powered by GenAI Fund" (25/07/2026) - xem chi tiết tại mục 4.2.


