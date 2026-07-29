---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:

* Triển khai luồng đăng ký/xác thực và cơ chế tự phục hồi `ensure_user_profile()` đã draft tuần trước.
* Fix bug rò rỉ dữ liệu multi-tenancy, bug lẫn session token, và các bug khác đã phát hiện tuần trước.
* Tự động hóa việc dọn dẹp tài khoản Cognito chưa xác thực bằng Amazon EventBridge.
* Thêm tính năng "Đăng nhập bằng Google" cho **Smart Docs AI**.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2-3 | - Triển khai luồng đăng ký/xác thực: chỉ tạo profile trong DynamoDB **sau khi** user xác thực email (`sign_up` → `UNCONFIRMED` → `confirm-signup` → `admin_get_user` → tạo profile) <br> - Thêm `ensure_user_profile()` tự phục hồi khi gọi `GET /api/profile` <br> - Code trang hiển thị thông tin user + đổi mật khẩu | 13/07/2026 | 14/07/2026 | |
| 4 | - Fix bug rò rỉ dữ liệu multi-tenancy: đổi đường dẫn FAISS vector store thành `vectorstore/{user_id}/...`, đường dẫn S3 thành `uploads/{user_id}/{filename}`, bỏ biến state toàn cục ở module level <br> - Fix bug phiên đăng nhập lẫn giữa các tab (chuyển từ `localStorage` sang `sessionStorage`, truyền rõ `Storage` cho `CognitoUser`) <br> - Xóa các test endpoint và hoàn thiện hạ tầng testing local cho toàn bộ profile endpoints <br> - Draft Blog 3 (Lambda Tenant Isolation Mode) nhân lúc fix bug multi-tenancy | 15/07/2026 | 15/07/2026 | |
| 5 | - Fix bug cập nhật thông tin cá nhân bị lỗi 400 (dùng email thay vì `sub` làm Username) <br> - Fix bug CORS che giấu lỗi 500 thật (thêm `exception_handler(Exception)` toàn cục), bug bộ lọc file bị bỏ qua ở Self-RAG/Co-RAG, và bug lặp lịch sử chat ở câu hỏi tiếp nối <br> - Tìm hiểu Amazon EventBridge Scheduled Rules và triển khai EventBridge rule (`rate(1 minute)`) gọi hàm Lambda `cleanup_unconfirmed_users()`, đã test thực tế (tạo user chưa xác thực, xác nhận bị xóa tự động sau ~6 phút; chi phí phát sinh gần như $0) <br> - Draft Blog 1 (EventBridge Scheduler vs Rule) nhân lúc triển khai rule cleanup | 16/07/2026 | 16/07/2026 | |
| 6 | - Nghiên cứu và cấu hình Google làm Identity Provider cho Cognito User Pool <br> - Thiết kế luồng OAuth redirect | 17/07/2026 | 17/07/2026 | |
| 7 | - Code phần Frontend đăng nhập Google (`cognitoOAuth.js`, `GoogleCallbackPage.jsx`): xử lý redirect, đổi authorization code lấy token <br> - Fix các trường hợp gộp tài khoản Google bị trùng email với user Cognito gốc <br> - Test đăng nhập bằng Google thành công | 18/07/2026 | 18/07/2026 | |


### Kết quả đạt được tuần 4:

* Triển khai thành công luồng tạo profile mới: DynamoDB chỉ lưu profile sau khi user xác thực email, tránh phát sinh "user rác" chưa xác nhận, có cơ chế tự phục hồi (`ensure_user_profile`) khi gặp race condition.
* Fix triệt để bug rò rỉ dữ liệu giữa các user (multi-tenancy): cô lập rõ ràng theo `user_id` ở cả FAISS vector store và S3, và fix bug phiên đăng nhập bị lẫn giữa các tab trình duyệt.
* Fix bug cập nhật thông tin cá nhân bị lỗi 400, bug CORS che giấu lỗi 500 thật, bug bộ lọc file bị bỏ qua ở Self-RAG/Co-RAG, và bug lặp lịch sử chat ở câu hỏi tiếp nối.
* Triển khai thành công EventBridge Scheduled Rule tự động dọn user Cognito chưa xác thực sau 5 phút, đã test thực tế và xác nhận hoạt động đúng; chi phí phát sinh gần như bằng 0.
* Thêm thành công tính năng "Đăng nhập bằng Google" cho **Smart Docs AI**, tích hợp Cognito Google Identity Provider, luồng OAuth redirect ở Frontend, và cơ chế gộp tài khoản Google/Cognito gốc trùng email.
* Draft Blog 3 (Lambda Tenant Isolation Mode: does this new feature solve multi-tenant data leak bugs?) và Blog 1 (EventBridge Scheduler: when should you "upgrade" from EventBridge Rule?) - xem chi tiết tại mục 3.3 và 3.1.


