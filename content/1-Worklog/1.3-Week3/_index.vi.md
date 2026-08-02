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
| 2-3 | - Review và test luồng xác thực Frontend của Trọng (Login form, Register form, Protected Route) <br>&emsp;+ Test thủ công từng luồng: đăng ký, đăng nhập, logout, truy cập route được bảo vệ khi chưa đăng nhập <br>&emsp;+ Mở song song 2 tab trình duyệt, đăng nhập 2 tài khoản khác nhau để kiểm tra tính độc lập giữa các phiên <br> - Ghi lại các vấn đề phát hiện được để fix vào tuần sau (ví dụ: phiên đăng nhập lẫn giữa các tab) <br>&emsp;+ Xác định sơ bộ nguyên nhân nghi ngờ là do cách lưu token ở `localStorage` (dùng chung mọi tab) thay vì `sessionStorage`, ghi chú lại để điều tra kỹ hơn tuần sau | 06/07/2026 | 07/07/2026 | |
| 4 | - Hoàn thiện diagram Kiến trúc Tổng quan trên AWS (`architecture-diagram.png`), mở rộng từ bản phác thảo sơ bộ Tuần 1 thành diagram đầy đủ 16 luồng (2 CI/CD pipeline, EventBridge cleanup, Cognito/Google OAuth), sau này dùng ở Proposal và mục 5.1.3 <br>&emsp;+ Đối chiếu diagram với AWS Well-Architected Framework để rà soát các luồng có đang bám sát nguyên tắc thiết kế serverless không (tách rõ compute/storage/network) <br>&emsp;+ Vẽ lại bằng draw.io với icon AWS chuẩn, đánh số thứ tự luồng để dễ giải thích trong Proposal <br> - Review việc đổi model Bedrock (`qwen.qwen3-next-80b-a3b`) và tối ưu upload file lớn của Nam <br>&emsp;+ Kiểm tra lại chất lượng câu trả lời sau khi đổi model, so sánh với model cũ trên cùng bộ câu hỏi test <br> - Xác định rủi ro rò rỉ dữ liệu multi-tenancy (đường dẫn FAISS/S3 dùng chung, chưa cô lập theo `user_id`) làm vấn đề thiết kế cần fix tuần sau <br>&emsp;+ Đọc lại tài liệu Lambda về execution environment lifecycle, xác nhận nguyên nhân gốc: Lambda tái sử dụng container "warm" giữa nhiều user khác nhau, nên biến global và path cố định (không có `user_id`) sẽ bị dùng chung <br>&emsp;+ Phác thảo hướng fix: thêm `user_id` vào path FAISS/S3 và bỏ biến `state` toàn cục, để tuần sau code chính thức <br> - Draft Blog 2 (Cold start) sau khi nhận thấy thời gian phản hồi của Co-RAG không ổn định lúc test <br>&emsp;+ Ghi lại số liệu đo thời gian phản hồi thực tế (có lần ~30s lỗi 503, có lần chỉ 5-10s) để làm dẫn chứng cho bài blog | 08/07/2026 | 08/07/2026 | [Lambda Execution Environment Lifecycle](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html) <br> [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html) |
| 5 | - Draft thiết kế luồng đăng ký/xác thực: chỉ tạo profile trong DynamoDB **sau khi** user xác thực email (`sign_up` → `UNCONFIRMED` → `confirm-signup` → `admin_get_user` → tạo profile), thêm cơ chế tự phục hồi `ensure_user_profile()` — chỉ dừng ở thiết kế, vì backend đăng ký/đăng nhập nền tảng chưa tồn tại <br>&emsp;+ So sánh với cách làm cũ (tạo profile ngay lúc `sign_up`, cần job dọn user chưa xác thực chạy nền) — nhận thấy job nền kiểu APScheduler sẽ không hoạt động trên Lambda vì mỗi request là 1 container mới, job không bao giờ chạy liên tục được <br>&emsp;+ Quyết định chọn dời việc tạo profile sang sau bước `confirm-signup`, để tránh phát sinh "user rác" trong DynamoDB nếu user bỏ ngang không xác thực <br>&emsp;+ Thiết kế `ensure_user_profile()` như một lớp tự phục hồi: nếu `GET /api/profile` không tìm thấy profile (do lỗi mạng giữa lúc `confirm-signup`), tự lấy lại attribute từ Cognito và tạo lại profile | 09/07/2026 | 09/07/2026 | [Signing up and confirming user accounts – Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/signing-up-users-in-your-app.html) |
| 6 | - Draft phương án fix bug CORS che giấu lỗi 500 thật, bug bộ lọc file bị bỏ qua ở Self-RAG/Co-RAG, và bug lặp lịch sử chat ở câu hỏi tiếp nối — ghi nhận là vấn đề đã biết, chưa fix <br>&emsp;+ Với bug CORS: nhận ra header CORS chỉ được thêm ở response thành công, nên khi backend lỗi 500 thật, trình duyệt lại báo nhầm thành lỗi CORS — hướng fix là thêm `exception_handler(Exception)` toàn cục để luôn trả CORS header kể cả khi lỗi <br>&emsp;+ Với bug bộ lọc file: xác định nguyên nhân do điều kiện lọc file bị bỏ qua khi chạy song song nhiều agent (Self-RAG/Co-RAG) <br>&emsp;+ Với bug lặp lịch sử chat: ghi nhận câu hỏi tiếp nối bị nối lại nhiều lần vào cùng 1 message thay vì tạo message mới | 10/07/2026 | 10/07/2026 | |
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


