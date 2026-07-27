---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:

* Tự động hóa việc dọn dẹp tài khoản Cognito chưa xác thực bằng Amazon EventBridge.
* Thêm tính năng "Đăng nhập bằng Google" cho **Smart Docs AI**.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2-3 | - Tìm hiểu Amazon EventBridge Scheduled Rule <br> - Thiết kế cơ chế tự động xóa user Cognito ở trạng thái `UNCONFIRMED` sau 5 phút | 13/07/2026 | 14/07/2026 | |
| 4 | - Triển khai EventBridge rule (`rate(1 minute)`) gọi Lambda <br> - Lambda phân nhánh theo `event.source == "aws.events"` để chạy `cleanup_unconfirmed_users()`, dùng `list_users(Filter=...)`, so sánh `UserCreateDate`, gọi `admin_delete_user` | 15/07/2026 | 15/07/2026 | |
| 5 | - Test thực tế cơ chế cleanup (tạo user chưa xác thực, xác nhận bị xóa tự động sau ~6 phút) <br> - Rà soát chi phí phát sinh (gần như $0, nằm trong Free Tier) | 16/07/2026 | 16/07/2026 | |
| 6 | - Nghiên cứu và cấu hình Google làm Identity Provider cho Cognito User Pool <br> - Thiết kế luồng OAuth redirect | 17/07/2026 | 17/07/2026 | |
| 7 | - Code phần Frontend đăng nhập Google (`cognitoOAuth.js`, `GoogleCallbackPage.jsx`): xử lý redirect, đổi authorization code lấy token <br> - Test đăng nhập bằng Google thành công | 18/07/2026 | 18/07/2026 | |


### Kết quả đạt được tuần 4:

* Triển khai thành công EventBridge Scheduled Rule tự động dọn user Cognito chưa xác thực sau 5 phút, đã test thực tế và xác nhận hoạt động đúng; chi phí phát sinh gần như bằng 0.
* Thêm thành công tính năng "Đăng nhập bằng Google" cho **Smart Docs AI**, tích hợp Cognito Google Identity Provider và luồng OAuth redirect ở Frontend.


