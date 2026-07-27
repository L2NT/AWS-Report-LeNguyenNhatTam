---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
### Mục tiêu tuần 3:

* Xây dựng luồng tạo hồ sơ (profile) người dùng gắn với xác thực email, tránh phát sinh dữ liệu rác khi user chưa xác nhận tài khoản.
* Rà soát và fix một loạt bug trong module RAG và quản lý profile của **Smart Docs AI**.
* Tham gia sự kiện cộng đồng "Cloud Architect x Meet Up".

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2-3 | - Thiết kế lại luồng đăng ký/xác thực: chỉ tạo profile trong DynamoDB **sau khi** user xác thực email (`sign_up` → `UNCONFIRMED` → `confirm-signup` → `admin_get_user` → tạo profile) <br> - Thêm `ensure_user_profile()` tự phục hồi khi gọi `GET /api/profile` | 06/07/2026 | 07/07/2026 | |
| 4 | - Fix bug rò rỉ dữ liệu multi-tenancy: đổi đường dẫn FAISS vector store thành `vectorstore/{user_id}/...`, đường dẫn S3 thành `uploads/{user_id}/{filename}`, bỏ biến state toàn cục ở module level | 08/07/2026 | 08/07/2026 | |
| 5 | - Fix bug phiên đăng nhập lẫn giữa các tab (chuyển từ `localStorage` sang `sessionStorage`, truyền rõ `Storage` cho `CognitoUser`) <br> - Fix bug trùng ID tài liệu FAISS khi upload file thứ 2 trở đi (reset id về `None` trước khi `FAISS.from_documents()`) | 09/07/2026 | 09/07/2026 | |
| 6 | - Fix bug CORS che giấu lỗi 500 thật (thêm `exception_handler(Exception)` toàn cục) <br> - Fix bug bộ lọc file bị bỏ qua ở Self-RAG/Co-RAG (thêm tham số `file_filter`) <br> - Fix bug lặp câu hỏi trong lịch sử chat khi hỏi tiếp nối | 10/07/2026 | 10/07/2026 | |
| 7 | - Fix bug cập nhật thông tin cá nhân bị lỗi 400 (dùng email thay vì `sub` làm Username) <br> - Tham gia sự kiện "Cloud Architect x Meet Up" | 11/07/2026 | 11/07/2026 | |


### Kết quả đạt được tuần 3:

* Triển khai thành công luồng tạo profile mới: DynamoDB chỉ lưu profile sau khi user xác thực email, tránh phát sinh "user rác" chưa xác nhận, có cơ chế tự phục hồi (`ensure_user_profile`) khi gặp race condition.
* Fix triệt để bug rò rỉ dữ liệu giữa các user (multi-tenancy): cô lập rõ ràng theo `user_id` ở cả FAISS vector store và S3.
* Fix bug phiên đăng nhập bị lẫn giữa các tab trình duyệt và bug trùng ID tài liệu khi upload nhiều file.
* Fix bug CORS che giấu lỗi 500 thật, giúp debug dễ dàng hơn nhiều.
* Fix bug bộ lọc file bị bỏ qua ở Self-RAG/Co-RAG và bug lặp lịch sử chat ở câu hỏi tiếp nối.
* Fix bug cập nhật thông tin cá nhân bị lỗi 400 do dùng sai định danh Username.
* Tham gia sự kiện "Cloud Architect x Meet Up" (11/07/2026) - xem chi tiết tại mục 4.1.


