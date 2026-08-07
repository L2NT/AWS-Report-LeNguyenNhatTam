---
title: "Nhật ký Tuần 4: Triển khai flow xác thực, fix phân lập dữ liệu & Đăng nhập Google"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:

* Triển khai flow đăng ký/xác thực và cơ chế tự phục hồi `ensure_user_profile()` đã lên thiết kế tuần trước.
* Fix lỗi rò rỉ dữ liệu đa người dùng (multi-tenancy), lỗi lẫn session token và các lỗi khác đã phát hiện tuần trước.
* Tự động hóa việc dọn dẹp tài khoản Cognito chưa xác thực bằng Amazon EventBridge.
* Tích hợp tính năng "Đăng nhập bằng Google" cho Smart Docs AI.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2-3 | - Triển khai flow đăng ký/xác thực: chỉ tạo profile trong DynamoDB sau khi người dùng xác thực email thành công <br>&emsp;+ Code endpoint đăng ký tài khoản trên Cognito <br>&emsp;+ Code endpoint xác thực mã OTP, xác thực xong mới lấy thông tin từ Cognito để tạo profile đầy đủ <br> - Bổ sung cơ chế tự phục hồi profile khi truy vấn thông tin người dùng, test mock lỗi đồng bộ (xóa profile thủ công rồi truy vấn lại, xác nhận hệ thống tự tạo lại từ Cognito) <br> - Code trang hiển thị thông tin người dùng và đổi mật khẩu, thêm kiểm tra mật khẩu mới theo chính sách Cognito (tối thiểu 8 ký tự, có hoa/thường/số) | 13/07/2026 | 14/07/2026 | [Signing up and confirming user accounts – Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/signing-up-users-in-your-app.html) |
| 4 | - Fix lỗi rò rỉ dữ liệu đa người dùng: tách riêng path lưu vector store và file trên S3 theo từng người dùng, bỏ việc dùng chung dữ liệu <br>&emsp;+ Thay cách giữ dữ liệu trong global variable bằng việc đọc lại trực tiếp từ storage riêng của từng người dùng ở mỗi lần truy vấn <br>&emsp;+ Test thực tế với 2 tài khoản: mỗi người chỉ thấy đúng file của mình, một người xóa hết file thì dữ liệu người còn lại vẫn nguyên vẹn <br> - Fix lỗi session lẫn giữa các tab bằng cách tách riêng cách lưu session theo từng tab, xác minh bằng cách đăng nhập 2 tài khoản khác nhau trên 2 tab <br> - Viết bộ test cho các chức năng profile (xem/cập nhật profile, đổi mật khẩu, tải ảnh đại diện) trước khi merge <br> - Soạn thảo Blog 3 (Lambda Tenant Isolation Mode) trong quá trình fix lỗi multi-tenancy | 15/07/2026 | 15/07/2026 | [Understanding the Lambda execution environment lifecycle](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html) |
| 5 | - Fix lỗi cập nhật thông tin cá nhân khi gọi Cognito admin API (nguyên nhân: user pool không bật alias email nên phải dùng đúng tên tài khoản thật là email) <br> - Fix lỗi 500 từ Backend bị báo nhầm thành lỗi CORS (thêm bước xử lý lỗi chung để response luôn kèm CORS header), lỗi file filter bị bỏ qua ở Self-RAG/Co-RAG, và lỗi lặp lịch sử chat ở câu hỏi follow-up <br> - Nghiên cứu EventBridge Scheduled Rules và triển khai tác vụ định kỳ gọi hàm Lambda tự động dọn tài khoản chưa xác thực, đã test thực tế (chi phí gần như bằng 0) <br> - Soạn thảo Blog 1 (EventBridge Scheduler vs Rule) trong quá trình triển khai tác vụ dọn dẹp | 16/07/2026 | 16/07/2026 | [Tutorial: Schedule a Lambda function – EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-run-lambda-schedule.html) |
| 6 | - Nghiên cứu và cấu hình Google làm Identity Provider cho Cognito User Pool <br>&emsp;+ Tạo OAuth 2.0 Client ID/Secret trên Google Cloud Console, khai báo đúng Authorized redirect URI trỏ về domain Cognito <br>&emsp;+ Thêm Google làm Social Identity Provider, cấu hình lấy các thông tin cần thiết (email, tên tài khoản) <br> - Thiết kế flow redirect OAuth: cân nhắc giữa Cognito Hosted UI có sẵn hay tự code màn hình riêng — chọn tự code để giữ giao diện đồng nhất | 17/07/2026 | 17/07/2026 | [Using social identity providers with a user pool – Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-social-idp.html) |
| 7 | - Code phần Frontend đăng nhập Google: xử lý redirect và đổi authorization code lấy token xác thực <br> - Xử lý trường hợp email Google trùng với tài khoản thường bằng Cognito Pre sign-up Lambda trigger: nếu email chưa có thì tạo tài khoản mới và tự xác nhận, nếu email đã có tài khoản thường thì tự động liên kết (link) Google làm provider bổ sung vào tài khoản Cognito đã có, gộp thành một tài khoản duy nhất <br> - Chiều ngược lại: khi đăng ký bằng email/mật khẩu mà email đó đã đăng nhập bằng Google thì chặn, yêu cầu đăng nhập bằng Google <br> - Test các trường hợp: email mới, email trùng tài khoản thường (được gộp) và đăng ký thường trên email đã dùng Google (bị chặn) | 18/07/2026 | 18/07/2026 | |


### Kết quả đạt được tuần 4:

* Triển khai thành công flow tạo profile mới: DynamoDB chỉ lưu profile sau khi xác thực email, tránh "dead account", có cơ chế tự phục hồi profile khi gặp lỗi đồng bộ.
* Fix lỗi rò rỉ dữ liệu giữa các người dùng (multi-tenancy): tách riêng dữ liệu lưu trữ theo từng người dùng, đồng thời fix lỗi session lẫn giữa các tab.
* Fix lỗi cập nhật thông tin cá nhân, lỗi 500 từ Backend bị báo nhầm thành CORS, lỗi file filter bị bỏ qua ở Self-RAG/Co-RAG, và lỗi lặp lịch sử chat.
* Triển khai thành công EventBridge Scheduled Rule tự động dọn tài khoản Cognito chưa xác thực, chi phí gần như bằng 0.
* Tích hợp thành công tính năng "Đăng nhập bằng Google" cho Smart Docs AI, kèm cơ chế tự liên kết (gộp) tài khoản Google vào tài khoản thường khi trùng email.
* Soạn thảo Blog 3 (Lambda Tenant Isolation Mode) và Blog 1 (EventBridge Scheduler) - xem chi tiết tại mục 3.3 và 3.1.


