---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
### Mục tiêu tuần 3:

* Review và test lại các phần việc gần đây của đồng đội: luồng xác thực Frontend của Trọng (Login/Register/Protected Route) và các tối ưu Bedrock/RAG của Nam.
* Hoàn thiện diagram Kiến trúc Tổng quan trên AWS dùng ở Proposal và mục 5.1.3, dựa trên bản phác thảo sơ bộ từ Tuần 1.
* Draft (chỉ thiết kế, chưa code) luồng đăng ký/xác thực và phương án fix bug rò rỉ dữ liệu multi-tenancy, để triển khai vào tuần sau.
* Tham gia sự kiện cộng đồng "Cloud Architect x Meet Up".

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2-3 | - Review và test luồng xác thực Frontend của Trọng (Login form, Register form, Protected Route) <br> - Ghi lại các vấn đề phát hiện được để fix vào tuần sau (ví dụ: phiên đăng nhập lẫn giữa các tab) | 06/07/2026 | 07/07/2026 | |
| 4 | - Hoàn thiện diagram Kiến trúc Tổng quan trên AWS (`architecture-diagram.png`), mở rộng từ bản phác thảo sơ bộ Tuần 1 thành diagram đầy đủ 16 luồng (2 CI/CD pipeline, EventBridge cleanup, Cognito/Google OAuth), sau này dùng ở Proposal và mục 5.1.3 <br> - Review việc đổi model Bedrock (`qwen.qwen3-next-80b-a3b`) và tối ưu upload file lớn của Nam <br> - Xác định rủi ro rò rỉ dữ liệu multi-tenancy (đường dẫn FAISS/S3 dùng chung, chưa cô lập theo `user_id`) làm vấn đề thiết kế cần fix tuần sau <br> - Draft Blog 2 (Cold start) sau khi nhận thấy thời gian phản hồi của Co-RAG không ổn định lúc test | 08/07/2026 | 08/07/2026 | |
| 5 | - Draft thiết kế luồng đăng ký/xác thực: chỉ tạo profile trong DynamoDB **sau khi** user xác thực email (`sign_up` → `UNCONFIRMED` → `confirm-signup` → `admin_get_user` → tạo profile), thêm cơ chế tự phục hồi `ensure_user_profile()` — chỉ dừng ở thiết kế, vì backend đăng ký/đăng nhập nền tảng chưa tồn tại | 09/07/2026 | 09/07/2026 | |
| 6 | - Draft phương án fix bug CORS che giấu lỗi 500 thật, bug bộ lọc file bị bỏ qua ở Self-RAG/Co-RAG, và bug lặp lịch sử chat ở câu hỏi tiếp nối — ghi nhận là vấn đề đã biết, chưa fix | 10/07/2026 | 10/07/2026 | |
| 7 | - Tham gia sự kiện "Cloud Architect x Meet Up" | 11/07/2026 | 11/07/2026 | |


### Kết quả đạt được tuần 3:

* Review và test luồng xác thực Frontend của Trọng (Login/Register/Protected Route), ghi nhận bug session token và các vấn đề khác để fix tuần sau.
* Review việc đổi model Bedrock và tối ưu upload file lớn cho pipeline RAG của Nam.
* Hoàn thiện diagram Kiến trúc Tổng quan trên AWS (16 luồng) dùng ở Proposal và mục 5.1.3, dựa trên bản phác thảo sơ bộ Tuần 1.
* Xác định rủi ro rò rỉ dữ liệu multi-tenancy và draft phương án fix (cô lập đường dẫn FAISS/S3 theo `user_id`) cho tuần sau.
* Draft thiết kế luồng đăng ký/xác thực và cơ chế tự phục hồi `ensure_user_profile()`.
* Draft phương án fix bug CORS che giấu lỗi 500, bug bộ lọc file bị bỏ qua ở Self-RAG/Co-RAG, và bug lặp lịch sử chat.
* Draft Blog 2 ("Cold start in serverless: why my chatbot occasionally fails to respond") - xem chi tiết tại mục 3.2.
* Tham gia sự kiện "Cloud Architect x Meet Up" (11/07/2026) - xem chi tiết tại mục 4.1.


