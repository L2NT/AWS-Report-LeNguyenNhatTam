---
title: "Nhật ký Tuần 3: Đánh giá công việc nhóm, hoàn thiện kiến trúc & Phân tích rủi ro"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
### Mục tiêu tuần 3:

* Rà soát và test các phần việc gần đây của đồng đội: flow xác thực Frontend (Đăng nhập/Đăng ký/Protected Route) và các tối ưu Bedrock/RAG.
* Hoàn thiện sơ đồ Kiến trúc Tổng quan trên AWS dùng ở Proposal và mục 5.1.3, dựa trên bản phác thảo sơ bộ từ Tuần 1.
* Phác thảo thiết kế (chưa code) flow đăng ký/xác thực và phương án fix lỗi rò rỉ dữ liệu đa người dùng (multi-tenancy) để triển khai vào tuần sau.
* Tham gia sự kiện cộng đồng "Cloud Architect x Meet Up".

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2-3 | - Rà soát và test flow xác thực Frontend do đồng đội làm (Login/Register/Protected Route) <br>&emsp;+ Test thủ công từng flow: đăng ký, đăng nhập, đăng xuất, truy cập route được bảo vệ khi chưa đăng nhập <br>&emsp;+ Mở 2 tab trình duyệt, đăng nhập 2 tài khoản khác nhau để kiểm tra tính độc lập giữa các session <br> - Ghi nhận các vấn đề để fix tuần sau (vd: session lẫn giữa các tab, nghi do cơ chế lưu session dùng chung giữa các tab thay vì tách riêng) | 06/07/2026 | 07/07/2026 | |
| 4 | - Hoàn thiện sơ đồ Kiến trúc Tổng quan trên AWS, mở rộng từ bản phác thảo Tuần 1 thành sơ đồ đầy đủ các flow (CI/CD pipeline, EventBridge cleanup, Cognito/Google OAuth) <br>&emsp;+ Đối chiếu sơ đồ với AWS Well-Architected Framework để rà soát các flow có bám nguyên tắc Serverless không <br>&emsp;+ Vẽ lại bằng draw.io với icon AWS chuẩn, đánh số flow để dễ giải thích trong Proposal <br> - Đánh giá việc đổi mô hình Bedrock và tối ưu tải file lớn của đồng đội, kiểm tra lại chất lượng câu trả lời so với mô hình cũ trên cùng bộ câu hỏi <br> - Xác định rủi ro rò rỉ dữ liệu đa người dùng (multi-tenancy) do dữ liệu tìm kiếm và file tải lên chưa tách riêng theo từng người dùng — vấn đề cần fix tuần sau <br>&emsp;+ Tìm hiểu cách Lambda tái sử dụng môi trường "warm" giữa nhiều người dùng, khiến dữ liệu dùng chung nếu không phân tách <br>&emsp;+ Phác thảo hướng fix: tách riêng path lưu trữ dữ liệu theo từng người dùng | 08/07/2026 | 08/07/2026 | [Lambda Execution Environment Lifecycle](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html) <br> [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html) |
| 5 | - Phác thảo thiết kế flow đăng ký/xác thực: chỉ tạo profile trong DynamoDB **sau khi** người dùng xác thực email, kèm cơ chế tự phục hồi profile — chỉ dừng ở thiết kế vì Backend xác thực nền tảng chưa tồn tại <br>&emsp;+ So sánh với cách cũ (tạo profile ngay khi đăng ký, cần tác vụ nền dọn tài khoản chưa xác thực) — tác vụ nền chạy định kỳ không ổn định trên Lambda do môi trường không chạy liên tục <br>&emsp;+ Dời việc tạo profile sang sau bước xác thực email để tránh "dead account" khi người dùng bỏ ngang <br>&emsp;+ Cơ chế tự phục hồi: nếu không tìm thấy profile khi truy vấn (do lỗi mạng giữa lúc xác thực), hệ thống tự lấy lại thông tin từ Cognito và tạo lại | 09/07/2026 | 09/07/2026 | [Signing up and confirming user accounts – Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/signing-up-users-in-your-app.html) |
| 6 | - Phác thảo phương án fix lỗi CORS che giấu lỗi hệ thống thật, lỗi file filter bị bỏ qua ở Self-RAG/Co-RAG, và lỗi lặp lịch sử trò chuyện ở follow-up <br>&emsp;+ Lỗi CORS: header CORS chỉ được thêm ở phản hồi thành công, nên khi Backend lỗi thật trình duyệt báo nhầm thành lỗi CORS — hướng fix là thêm bước xử lý lỗi chung để luôn trả đúng header <br>&emsp;+ Lỗi file filter: do điều kiện lọc file bị bỏ qua khi chạy song song nhiều chế độ hỏi đáp <br>&emsp;+ Lỗi lặp lịch sử chat: follow-up bị nối lại nhiều lần thay vì tạo mục trò chuyện mới | 10/07/2026 | 10/07/2026 | |
| 7 | - Tham gia sự kiện "Cloud Architect x Meet Up" | 11/07/2026 | 11/07/2026 | |


### Kết quả đạt được tuần 3:

* Rà soát và test flow xác thực Frontend (Login/Register/Protected Route), ghi nhận lỗi lẫn session giữa các tab và các vấn đề khác để fix tuần sau.
* Đánh giá việc đổi mô hình Bedrock và tối ưu tải file lớn cho pipeline RAG.
* Hoàn thiện sơ đồ Kiến trúc Tổng quan trên AWS dùng ở Proposal và mục 5.1.3.
* Xác định rủi ro rò rỉ dữ liệu đa người dùng (multi-tenancy) và phác thảo phương án fix (tách riêng dữ liệu lưu trữ theo từng người dùng) cho tuần sau.
* Phác thảo thiết kế flow đăng ký/xác thực và cơ chế tự phục hồi profile người dùng.
* Phác thảo phương án fix lỗi CORS che giấu lỗi 500, lỗi file filter bị bỏ qua ở Self-RAG/Co-RAG, và lỗi lặp lịch sử chat.
* Tham gia sự kiện "Cloud Architect x Meet Up" (11/07/2026) - xem chi tiết tại mục 4.1.


