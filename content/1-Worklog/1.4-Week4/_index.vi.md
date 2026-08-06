---
title: "Nhật ký Tuần 4: Triển khai luồng xác thực, fix phân lập dữ liệu & Đăng nhập Google"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:

* Triển khai luồng đăng ký/xác thực và cơ chế tự phục hồi `ensure_user_profile()` đã phác thảo tuần trước.
* Fix lỗi rò rỉ dữ liệu đa người dùng (multi-tenancy), lỗi lẫn session token và các lỗi khác đã phát hiện tuần trước.
* Tự động hóa việc dọn dẹp tài khoản Cognito chưa xác thực bằng Amazon EventBridge.
* Tích hợp tính năng "Đăng nhập bằng Google" cho **Smart Docs AI**.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2-3 | - Triển khai luồng đăng ký/xác thực: chỉ tạo hồ sơ người dùng trong DynamoDB **sau khi** người dùng xác thực email thành công <br>&emsp;+ Code endpoint đăng ký tài khoản trên Cognito <br>&emsp;+ Code endpoint xác thực mã OTP, sau khi xác thực thành công mới lấy thông tin từ Cognito để tạo hồ sơ đầy đủ <br> - Bổ sung cơ chế tự phục hồi hồ sơ khi truy vấn thông tin người dùng <br>&emsp;+ Kiểm thử giả lập tình huống đồng bộ lỗi: xóa hồ sơ thủ công rồi truy vấn lại, xác nhận hệ thống tự tạo lại hồ sơ từ thông tin Cognito <br> - Code trang hiển thị thông tin người dùng và đổi mật khẩu <br>&emsp;+ Thêm kiểm tra mật khẩu mới theo chính sách của Cognito (tối thiểu 8 ký tự, có hoa/thường/số) | 13/07/2026 | 14/07/2026 | [Signing up and confirming user accounts – Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/signing-up-users-in-your-app.html) |
| 4 | - Fix lỗi rò rỉ dữ liệu đa người dùng: tách riêng đường dẫn lưu vector store và tệp trên S3 theo từng người dùng, bỏ việc dùng chung dữ liệu <br>&emsp;+ Thay cách giữ dữ liệu trong biến toàn cục bằng việc đọc lại trực tiếp từ kho lưu trữ riêng của từng người dùng ở mỗi lần truy vấn <br>&emsp;+ Kiểm thử thực tế với 2 tài khoản: mỗi người dùng chỉ thấy đúng tệp của mình, một người xóa hết tệp thì dữ liệu người còn lại vẫn nguyên vẹn <br> - Fix lỗi phiên đăng nhập lẫn giữa các tab trình duyệt bằng cách tách riêng cách lưu phiên theo từng tab <br>&emsp;+ Xác minh lại bằng cách đăng nhập 2 tài khoản khác nhau trên 2 tab <br> - Viết bộ kiểm thử cho các chức năng hồ sơ người dùng (xem/cập nhật hồ sơ, đổi mật khẩu, tải ảnh đại diện) trước khi hợp nhất <br> - Soạn thảo Blog 3 (Lambda Tenant Isolation Mode) nhân lúc fix lỗi multi-tenancy | 15/07/2026 | 15/07/2026 | [Understanding the Lambda execution environment lifecycle](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html) |
| 5 | - Fix lỗi cập nhật thông tin cá nhân khi gọi Cognito admin API <br>&emsp;+ Xác định nguyên nhân: user pool không bật alias email nên phải dùng đúng tên tài khoản thật (email) khi gọi API quản trị <br> - Fix lỗi CORS che giấu lỗi hệ thống thật (thêm bước xử lý lỗi chung), lỗi bộ lọc tệp bị bỏ qua ở Self-RAG/Co-RAG, và lỗi lặp lịch sử chat ở câu hỏi tiếp nối <br>&emsp;+ Kiểm thử lại từng lỗi bằng cách giả lập lỗi hệ thống, kiểm tra trình duyệt hiển thị đúng lỗi thay vì báo CORS <br> - Nghiên cứu Amazon EventBridge Scheduled Rules và triển khai tác vụ định kỳ gọi hàm Lambda tự động dọn tài khoản chưa xác thực, đã kiểm thử thực tế (tạo tài khoản chưa xác thực, xác nhận bị xóa tự động; chi phí phát sinh gần như bằng 0) <br>&emsp;+ Thiết kế hàm Lambda để phân biệt được lời gọi từ EventBridge với request HTTP thông thường qua API Gateway <br> - Soạn thảo Blog 1 (EventBridge Scheduler vs Rule) nhân lúc triển khai tác vụ dọn dẹp | 16/07/2026 | 16/07/2026 | [Tutorial: Schedule a Lambda function – EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-run-lambda-schedule.html) |
| 6 | - Nghiên cứu và cấu hình Google làm Identity Provider cho Cognito User Pool <br>&emsp;+ Tạo OAuth 2.0 Client ID/Secret trên Google Cloud Console, khai báo đúng Authorized redirect URI trỏ về domain Cognito <br>&emsp;+ Thêm Google làm Social Identity Provider trong Cognito User Pool, cấu hình lấy các thông tin cần thiết (email, tên tài khoản) <br> - Thiết kế luồng chuyển hướng OAuth <br>&emsp;+ Cân nhắc giữa dùng Cognito Hosted UI có sẵn hay tự code màn hình riêng — quyết định tự code để giữ giao diện đồng nhất với phần còn lại của ứng dụng | 17/07/2026 | 17/07/2026 | [Using social identity providers with a user pool – Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-social-idp.html) |
| 7 | - Code phần Frontend đăng nhập Google: xử lý chuyển hướng và đổi mã ủy quyền lấy token xác thực <br> - Fix các trường hợp tài khoản Google bị trùng email với tài khoản thường đã có <br>&emsp;+ Nhận thấy tài khoản Google được lưu khác với tài khoản thường (vốn dùng email làm tên đăng nhập) — bổ sung bước kiểm tra email trùng, chặn đăng nhập Google nếu email đã thuộc về một tài khoản thường khác <br> - Kiểm thử đăng nhập bằng Google thành công <br>&emsp;+ Kiểm thử cả 2 trường hợp: email mới hoàn toàn (tạo tài khoản mới) và email trùng với tài khoản thường đã có (bị chặn đúng như thiết kế) | 18/07/2026 | 18/07/2026 | |


### Kết quả đạt được tuần 4:

* Triển khai thành công luồng tạo hồ sơ mới: DynamoDB chỉ lưu hồ sơ sau khi người dùng xác thực email, tránh phát sinh "tài khoản rác" chưa xác nhận, có cơ chế tự phục hồi hồ sơ khi gặp lỗi đồng bộ.
* Fix triệt để lỗi rò rỉ dữ liệu giữa các người dùng (multi-tenancy): tách riêng rõ ràng dữ liệu lưu trữ theo từng người dùng, đồng thời fix lỗi phiên đăng nhập bị lẫn giữa các tab trình duyệt.
* Fix lỗi cập nhật thông tin cá nhân, lỗi CORS che giấu lỗi hệ thống thật, lỗi bộ lọc tệp bị bỏ qua ở Self-RAG/Co-RAG, và lỗi lặp lịch sử chat ở câu hỏi tiếp nối.
* Triển khai thành công EventBridge Scheduled Rule tự động dọn tài khoản Cognito chưa xác thực, đã kiểm thử thực tế và xác nhận hoạt động đúng; chi phí phát sinh gần như bằng 0.
* Tích hợp thành công tính năng "Đăng nhập bằng Google" cho **Smart Docs AI** gồm Cognito Google Identity Provider, luồng OAuth redirect ở Frontend và cơ chế gộp tài khoản Google/Cognito gốc trùng email.
* Soạn thảo Blog 3 (Lambda Tenant Isolation Mode) và Blog 1 (EventBridge Scheduler) - xem chi tiết tại mục 3.3 và 3.1.


