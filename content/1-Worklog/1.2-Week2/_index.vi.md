---
title: "Nhật ký Tuần 2: Nghiên cứu các dịch vụ lưu trữ, mở rộng & xác thực"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
### Mục tiêu tuần 2:

* Hoàn thiện và tối ưu lại giao diện Frontend của Smart Docs AI.
* Nghiên cứu dịch vụ Amazon S3 (quản lý bucket/object, lưu trữ website tĩnh, tích hợp CloudFront).
* Nghiên cứu Amazon RDS và EC2 Auto Scaling phục vụ khả năng mở rộng ứng dụng.
* Tìm hiểu AWS KMS và Amazon Cognito, chuẩn bị nền tảng cho phần xác thực người dùng ở Backend.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2-3 | - Tối ưu lại giao diện Frontend của Smart Docs AI <br>&emsp;+ Tách lại các thành phần giao diện cho gọn hơn, chuẩn hoá lại bảng màu/khoảng cách bằng Tailwind để dễ mở rộng giao diện về sau <br> - Nghiên cứu Amazon S3: bucket/object, lưu trữ website tĩnh, chặn/cho phép truy cập công khai <br>&emsp;+ So sánh 2 phương án lưu trữ Frontend: S3 static website hosting (đơn giản, chỉ HTTP) với S3 + CloudFront (có HTTPS, cache toàn cầu) — quyết định chọn phương án sau vì cần HTTPS cho luồng OAuth callback của Cognito <br> - **Thực hành:** kích hoạt CloudFront trước website tĩnh <br>&emsp;+ Tạo CloudFront distribution trỏ về S3 bucket, cấu hình Origin Access Control (OAC) để chặn truy cập S3 trực tiếp, chỉ cho phép qua CloudFront | 29/06/2026 | 30/06/2026 | [Hướng dẫn Amazon S3](https://000057.awsstudygroup.com/vi/) |
| 4 | - Tìm hiểu khái niệm Amazon RDS & Aurora <br>&emsp;+ So sánh RDS (managed engine truyền thống: MySQL/PostgreSQL...) với Aurora (tương thích MySQL/PostgreSQL nhưng hiệu năng cao hơn, tự scale storage) <br>&emsp;+ Nhận thấy Smart Docs AI thiên về lưu metadata tài liệu dạng key-value hơn là quan hệ phức tạp — ghi chú cân nhắc DynamoDB thay vì RDS khi thiết kế backend thật <br> - Đọc tài liệu về triển khai, backup, restore RDS <br>&emsp;+ Nắm cơ chế automated backup + snapshot thủ công, retention period mặc định — làm nền so sánh với on-demand backup của DynamoDB sau này | 01/07/2026 | 01/07/2026 | [Hướng dẫn Amazon RDS](https://000005.awsstudygroup.com/vi/) |
| 5 | - Tìm hiểu EC2 Auto Scaling: Auto Scaling Group, Launch Template, Elastic Load Balancer, Target Group <br>&emsp;+ Hiểu cơ chế scale theo CloudWatch metric (CPU vượt ngưỡng → tự thêm instance), ELB phân phối traffic qua Target Group tới các instance đang healthy <br> - Tổng quan EFS/FSx/Lightsail <br>&emsp;+ Ghi chú EFS phù hợp khi cần nhiều EC2/container cùng đọc-ghi 1 file system chung — liên hệ đến nhu cầu lưu file tài liệu dùng chung của Smart Docs AI (dù cuối cùng chọn S3 vì rẻ và đã quen) | 02/07/2026 | 02/07/2026 | [EC2 Auto Scaling](https://000006.awsstudygroup.com/vi/) |
| 6 | - Tìm hiểu AWS KMS (quản lý khóa mã hóa) và Amazon Cognito (user pool, luồng đăng ký/đăng nhập) chuẩn bị cho phần xác thực ở Backend <br>&emsp;+ Nắm khái niệm Customer Managed Key và AWS Managed Key trong KMS, dùng cho việc mã hóa DynamoDB ở các tuần sau <br>&emsp;+ Tìm hiểu luồng User Pool cơ bản của Cognito (đăng ký → xác nhận email → đăng nhập) — nền tảng cho toàn bộ luồng xác thực của dự án | 03/07/2026 | 03/07/2026 | [Amazon Cognito](https://000081.awsstudygroup.com/vi/) |
| 7 | - Hoàn thiện, cập nhật Worklog tuần 1 và tuần 2 <br>&emsp;+ Rà lại các mục đã làm trong tuần, đối chiếu ngày tháng cho khớp thực tế <br> - Đồng bộ toàn bộ mã nguồn và tài liệu lên GitHub | 04/07/2026 | 04/07/2026 | Personal GitHub Repository |


### Kết quả đạt được tuần 2:

* Hoàn thiện lại giao diện Frontend Smart Docs AI, cải thiện bố cục và trải nghiệm người dùng.
* Nắm được cách hoạt động của Amazon S3: tạo/quản lý bucket, upload object, cấu hình static website hosting, tích hợp CloudFront.
* Nắm vững kiến thức nền tảng về Amazon RDS: vận hành, backup, restore.
* Hiểu cơ chế mở rộng ứng dụng bằng EC2 Auto Scaling (Auto Scaling Group, Launch Template, ELB, Target Group).
* Tìm hiểu AWS KMS (quản lý khóa mã hóa) và Amazon Cognito (user pool, luồng đăng ký/đăng nhập) - nền tảng cho phần xác thực của dự án ở các tuần sau.
* Hoàn thiện và đồng bộ đầy đủ Worklog tuần 1, tuần 2 lên GitHub.


