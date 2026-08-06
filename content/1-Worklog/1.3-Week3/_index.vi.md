---
title: "Nhật ký Tuần 3: Đánh giá công việc nhóm, hoàn thiện kiến trúc & Phân tích rủi ro"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
### Mục tiêu tuần 3:

* Rà soát và kiểm thử các phần việc gần đây của đồng đội: luồng xác thực Frontend (Đăng nhập/Đăng ký/Protected Route) và các tối ưu Bedrock/RAG.
* Hoàn thiện sơ đồ Kiến trúc Tổng quan trên AWS dùng ở Proposal và mục 5.1.3, dựa trên bản phác thảo sơ bộ từ Tuần 1.
* Phác thảo thiết kế (chưa code) luồng đăng ký/xác thực và phương án fix lỗi rò rỉ dữ liệu đa người dùng (multi-tenancy) để triển khai vào tuần sau.
* Tham gia sự kiện cộng đồng "Cloud Architect x Meet Up".

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2-3 | - Rà soát và kiểm thử luồng xác thực Frontend do đồng đội làm (Login form, Register form, Protected Route) <br>&emsp;+ Kiểm thử thủ công từng luồng: đăng ký, đăng nhập, đăng xuất, truy cập route được bảo vệ khi chưa đăng nhập <br>&emsp;+ Mở song song 2 tab trình duyệt, đăng nhập 2 tài khoản khác nhau để kiểm tra tính độc lập giữa các phiên <br> - Ghi nhận các vấn đề phát hiện được để fix vào tuần sau (ví dụ: phiên đăng nhập lẫn giữa các tab) <br>&emsp;+ Xác định sơ bộ nguyên nhân nghi ngờ do cơ chế lưu phiên đăng nhập dùng chung giữa các tab trình duyệt thay vì tách riêng theo từng tab | 06/07/2026 | 07/07/2026 | |
| 4 | - Hoàn thiện sơ đồ Kiến trúc Tổng quan trên AWS, mở rộng từ bản phác thảo sơ bộ Tuần 1 thành sơ đồ đầy đủ các luồng (CI/CD pipeline, EventBridge cleanup, Cognito/Google OAuth) <br>&emsp;+ Đối chiếu sơ đồ với AWS Well-Architected Framework để rà soát các luồng có bám sát nguyên tắc thiết kế Serverless không <br>&emsp;+ Vẽ lại bằng draw.io với bộ icon AWS chuẩn, đánh số thứ tự luồng để dễ giải thích trong Proposal <br> - Đánh giá việc đổi mô hình Bedrock và tối ưu tải tệp lớn của đồng đội <br>&emsp;+ Kiểm tra lại chất lượng câu trả lời sau khi đổi mô hình, so sánh với mô hình cũ trên cùng bộ câu hỏi kiểm thử <br> - Xác định rủi ro rò rỉ dữ liệu đa người dùng (multi-tenancy) do dữ liệu tìm kiếm tài liệu và tệp tải lên chưa được tách riêng theo từng người dùng — đây là vấn đề thiết kế cần fix tuần sau <br>&emsp;+ Tìm hiểu cách Lambda tái sử dụng môi trường chạy giữa các lần gọi, xác nhận nguyên nhân gốc: Lambda tái sử dụng môi trường "warm" giữa nhiều người dùng khác nhau, khiến dữ liệu dùng chung nếu không phân tách theo từng người dùng <br>&emsp;+ Phác thảo hướng fix: tách riêng đường dẫn lưu trữ dữ liệu theo từng người dùng, để tuần sau triển khai chính thức <br> - Soạn thảo Blog 2 (Cold start) sau khi nhận thấy thời gian phản hồi của Co-RAG không ổn định lúc kiểm thử <br>&emsp;+ Ghi lại số liệu đo thời gian phản hồi thực tế làm dẫn chứng cho bài viết | 08/07/2026 | 08/07/2026 | [Lambda Execution Environment Lifecycle](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html) <br> [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html) |
| 5 | - Phác thảo thiết kế luồng đăng ký/xác thực: chỉ tạo hồ sơ người dùng trong DynamoDB **sau khi** người dùng xác thực email thành công, kèm cơ chế tự phục hồi hồ sơ — chỉ dừng ở bước thiết kế, vì Backend xác thực nền tảng chưa tồn tại <br>&emsp;+ So sánh với cách làm cũ (tạo hồ sơ ngay khi đăng ký, cần tác vụ nền dọn tài khoản chưa xác thực) — nhận thấy tác vụ nền chạy định kỳ không hoạt động ổn định trên Lambda do môi trường thực thi không chạy liên tục <br>&emsp;+ Quyết định dời việc tạo hồ sơ sang sau bước xác thực email, để tránh phát sinh "tài khoản rác" nếu người dùng bỏ ngang không xác thực <br>&emsp;+ Thiết kế cơ chế tự phục hồi: nếu không tìm thấy hồ sơ khi truy vấn (do lỗi mạng giữa lúc xác thực), hệ thống tự lấy lại thông tin từ Cognito và tạo lại hồ sơ | 09/07/2026 | 09/07/2026 | [Signing up and confirming user accounts – Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/signing-up-users-in-your-app.html) |
| 6 | - Phác thảo phương án fix lỗi CORS che giấu lỗi hệ thống thật, lỗi bộ lọc tệp bị bỏ qua ở Self-RAG/Co-RAG, và lỗi lặp lịch sử trò chuyện ở câu hỏi tiếp nối <br>&emsp;+ Với lỗi CORS: nhận ra header CORS chỉ được thêm ở phản hồi thành công, nên khi Backend gặp lỗi thật, trình duyệt lại báo nhầm thành lỗi CORS — hướng fix là thêm bước xử lý lỗi chung cho toàn hệ thống để luôn trả đúng header kể cả khi lỗi <br>&emsp;+ Với lỗi bộ lọc tệp: xác định nguyên nhân do điều kiện lọc tệp bị bỏ qua khi chạy song song nhiều chế độ hỏi đáp (Self-RAG/Co-RAG) <br>&emsp;+ Với lỗi lặp lịch sử chat: ghi nhận câu hỏi tiếp nối bị nối lại nhiều lần thay vì tạo mục trò chuyện mới | 10/07/2026 | 10/07/2026 | |
| 7 | - Tham gia sự kiện "Cloud Architect x Meet Up" | 11/07/2026 | 11/07/2026 | |


### Kết quả đạt được tuần 3:

* Rà soát và kiểm thử luồng xác thực Frontend (Login/Register/Protected Route), ghi nhận lỗi lẫn phiên đăng nhập giữa các tab và các vấn đề khác để fix tuần sau.
* Đánh giá việc đổi mô hình Bedrock và tối ưu tải tệp lớn cho pipeline RAG.
* Hoàn thiện sơ đồ Kiến trúc Tổng quan trên AWS dùng ở Proposal và mục 5.1.3, dựa trên bản phác thảo sơ bộ Tuần 1.
* Xác định rủi ro rò rỉ dữ liệu đa người dùng (multi-tenancy) và phác thảo phương án fix (tách riêng dữ liệu lưu trữ theo từng người dùng) cho tuần sau.
* Phác thảo thiết kế luồng đăng ký/xác thực và cơ chế tự phục hồi hồ sơ người dùng.
* Phác thảo phương án fix lỗi CORS che giấu lỗi 500, lỗi bộ lọc tệp bị bỏ qua ở Self-RAG/Co-RAG, và lỗi lặp lịch sử chat.
* Soạn thảo Blog 2 ("Cold start in serverless: why my chatbot occasionally fails to respond") - xem chi tiết tại mục 3.2.
* Tham gia sự kiện "Cloud Architect x Meet Up" (11/07/2026) - xem chi tiết tại mục 4.1.


