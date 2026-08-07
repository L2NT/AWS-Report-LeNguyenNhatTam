---
title: "Nhật ký Tuần 1: Nghiên cứu tổng quan AWS Cloud & Lựa chọn đề tài"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Mục tiêu tuần 1:

* Làm quen thành viên chương trình First Cloud AI Journey (FCAJ) và nắm quy trình làm việc trong kỳ thực tập.
* Nghiên cứu kiến thức nền tảng AWS Cloud, hạ tầng toàn cầu và các công cụ quản lý.
* Thực hành bảo mật tài khoản (MFA) và phân quyền IAM.
* Thảo luận nhóm, chốt đề tài **Smart Docs AI** và làm giao diện Frontend ban đầu.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Làm quen thành viên FCAJ, đọc nội quy thực tập <br>&emsp;+ Nắm lịch làm việc, quy trình báo cáo và deadline nộp Worklog hàng tuần <br> - Xem "First Cloud Journey Kick off 2024", hướng dẫn vẽ kiến trúc AWS bằng Draw.io và làm Workshop <br>&emsp;+ Cài Hugo, làm quen tổ chức thư mục và cú pháp Markdown <br> - Dựng khung Workshop report, cập nhật thông tin cá nhân <br>&emsp;+ Khởi tạo từ mẫu, chạy thử ở máy cục bộ trước khi đồng bộ lên GitHub | 22/06/2026 | 22/06/2026 | [Kick off](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) <br> [Hướng dẫn Draw.io](https://www.youtube.com/watch?v=l8isyDe-GwY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=2) <br> [Hướng dẫn Workshop](https://www.youtube.com/watch?v=mXRqgMr_97U&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=3) |
| 3 | - Học điện toán đám mây, điểm khác biệt của AWS, hạ tầng toàn cầu (Region/AZ/Edge Location), công cụ quản lý (Console/CLI/SDK) <br>&emsp;+ Phân biệt Region/AZ/Edge Location, hiểu vì sao AWS dùng multi-AZ để đảm bảo high availability <br>&emsp;+ So sánh Console/CLI/SDK — quyết định học CLI song song Console ngay từ đầu <br> - Tổng quan các nhóm dịch vụ AWS: Compute/Storage/Networking/Database <br>&emsp;+ Ghi chú dịch vụ tiêu biểu mỗi nhóm làm cơ sở chọn kiến trúc sau này <br> - **Thực hành:** tạo AWS Free Tier, bật MFA, tạo AWS Budget <br>&emsp;+ Bật MFA ngay từ đầu để bảo vệ root account, đặt Budget cảnh báo $5/tháng phòng quên tắt tài nguyên | 23/06/2026 | 23/06/2026 | [Khái niệm Cloud](https://www.youtube.com/watch?v=HxYZAK1coOI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=4) <br> [AWS Free Tier](https://000001.awsstudygroup.com/vi/) <br> [AWS Budgets](https://000007.awsstudygroup.com/vi/) |
| 4 | - Học IAM: Group/User/Policy/Role <br>&emsp;+ Nắm nguyên tắc least privilege — gắn Policy vào Group/Role thay vì trực tiếp vào User <br> - **Thực hành:** tạo IAM Group/User/Role, chuyển đổi Role <br>&emsp;+ Tạo Group với Policy quyền hạn chế, tạo User riêng thay vì dùng chung root account; thử chuyển Role để hiểu cơ chế cấp quyền tạm thời | 24/06/2026 | 24/06/2026 | [AWS IAM](https://000002.awsstudygroup.com/vi/) |
| 5 | - **Thảo luận nhóm:** chốt đề tài **Smart Docs AI** và bộ công nghệ (ReactJS, Python, AWS) <br>&emsp;+ Cân nhắc vài ý tưởng ban đầu — chọn RAG chatbot xử lý tài liệu vì bám xu hướng GenAI và tận dụng được Amazon Bedrock <br>&emsp;+ Thống nhất ReactJS + Python/FastAPI + kiến trúc Serverless AWS để tối ưu chi phí <br> - Phác thảo giao diện sơ bộ (Wireframe) <br>&emsp;+ Dựng nhanh các màn hình chính (đăng nhập, tải tài liệu, khung chat) để thống nhất flow trải nghiệm trước khi code | 25/06/2026 | 25/06/2026 | |
| 6 | - Code các thành phần giao diện Frontend ban đầu <br>&emsp;+ Tạo dự án bằng ReactJS, làm các thành phần khung theo Wireframe <br> - Đồng bộ mã nguồn lên GitHub của nhóm <br>&emsp;+ Thống nhất quy tắc quản lý nhánh: mỗi người một nhánh, tạo Pull Request để rà soát trước khi merge | 26/06/2026 | 26/06/2026 | Repo GitHub dự án nhóm |
| 7 | - Nghiên cứu Amazon EC2 cơ bản: các loại instance, AMI, EBS <br>&emsp;+ Phân biệt họ instance burstable (rẻ) và hiệu năng cao, ưu tiên Free Tier cho thực hành <br> - Tổng quan AWS Cloud9 <br>&emsp;+ Thử môi trường Cloud9 mẫu, dù cuối cùng chọn code ở máy cục bộ và đồng bộ qua GitHub | 27/06/2026 | 27/06/2026 | [AWS Cloud9](https://000049.awsstudygroup.com/vi/) |


### Kết quả đạt được tuần 1:

* Làm quen thành viên FCAJ, nắm quy trình làm việc trong kỳ thực tập.
* Nắm kiến thức nền tảng AWS Cloud: hạ tầng toàn cầu, các nhóm dịch vụ chính, công cụ quản lý.
* Tạo tài khoản AWS Free Tier, bật MFA, thiết lập AWS Budgets kiểm soát chi phí.
* Hiểu và thực hành phân quyền IAM (Group/User/Policy/Role).
* Chốt đề tài **Smart Docs AI**, thống nhất bộ công nghệ (ReactJS, Python, AWS) cùng nhóm.
* Hoàn thành khung giao diện Frontend ban đầu và đồng bộ lên GitHub.
* Làm quen sơ bộ Amazon EC2, chuẩn bị cho tuần tiếp theo.


