---
title: "Worklog Tuần 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Mục tiêu tuần 1:

* Kết nối, làm quen với các thành viên First Cloud AI Journey (FCAJ) và nắm quy trình làm việc trong kỳ thực tập.
* Nắm vững kiến thức nền tảng AWS Cloud, hạ tầng toàn cầu và các công cụ quản lý cốt lõi.
* Thực hành bảo mật tài khoản (MFA), IAM và networking (VPC).
* Cả nhóm thảo luận và chốt đề tài **Smart Docs AI**, sau đó bắt tay vào phần frontend ban đầu.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Làm quen các thành viên FCAJ, đọc nội quy thực tập <br>&emsp;+ Tự giới thiệu bản thân trong nhóm chat chung, nắm lịch làm việc online/offline theo tuần <br>&emsp;+ Đọc kỹ nội quy: giờ báo cáo, quy trình xin nghỉ, deadline nộp Worklog hàng tuần <br> - Xem "First Cloud Journey Kick off 2024", hướng dẫn vẽ kiến trúc AWS bằng Draw.io, hướng dẫn làm Workshop (cài Hugo, cấu trúc thư mục, cú pháp Markdown) <br>&emsp;+ Cài Hugo Extended + theme hugo-theme-learn theo hướng dẫn, chạy thử `hugo server` ở local <br>&emsp;+ Nắm cấu trúc thư mục `content/` (mỗi mục có cặp file `_index.md`/`_index.vi.md` song ngữ) và cú pháp shortcode riêng của theme <br> - Dựng khung Workshop report, cập nhật thông tin giới thiệu bản thân <br>&emsp;+ Clone repo mẫu, đổi lại các mục theo cấu trúc cá nhân, cập nhật `config.toml` (tên, logo, thông tin liên hệ) <br>&emsp;+ Build thử local thành công trước khi push commit đầu tiên | 22/06/2026 | 22/06/2026 | [Kick off](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) <br> [Hướng dẫn Draw.io](https://www.youtube.com/watch?v=l8isyDe-GwY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=2) <br> [Hướng dẫn Workshop](https://www.youtube.com/watch?v=mXRqgMr_97U&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=3) |
| 3 | - Học điện toán đám mây là gì, điều gì tạo nên sự khác biệt của AWS, hạ tầng toàn cầu AWS (Region/AZ/Edge Location), công cụ quản lý AWS (Console/CLI/SDK) <br>&emsp;+ Phân biệt Region/Availability Zone/Edge Location, hiểu vì sao AWS dùng multi-AZ để đảm bảo high availability <br>&emsp;+ So sánh Console (trực quan, học nhanh) với CLI (tự động hoá, cần cho script deploy sau này) và SDK (tích hợp vào code) — quyết định học CLI song song Console ngay từ đầu <br> - Tổng quan các nhóm dịch vụ AWS: Compute/Storage/Networking/Database <br>&emsp;+ Ghi chú dịch vụ tiêu biểu mỗi nhóm (EC2/Lambda, S3/EBS, VPC, RDS/DynamoDB) làm cơ sở chọn kiến trúc cho Smart Docs AI sau này <br> - **Thực hành:** tạo AWS Free Tier account, bật MFA, tạo AWS Budget <br>&emsp;+ Bật MFA bằng Google Authenticator ngay từ đầu để tránh mất quyền kiểm soát root account <br>&emsp;+ Tạo AWS Budget cảnh báo ở ngưỡng $5/tháng, phòng trường hợp quên tắt tài nguyên demo | 23/06/2026 | 23/06/2026 | [Khái niệm Cloud](https://www.youtube.com/watch?v=HxYZAK1coOI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=4) <br> [AWS Free Tier](https://000001.awsstudygroup.com/vi/) <br> [AWS Budgets](https://000007.awsstudygroup.com/vi/) |
| 4 | - Học IAM: khái niệm Group/User/Policy/Role <br>&emsp;+ Nắm nguyên tắc least privilege — Policy nên gắn vào Group/Role thay vì gắn trực tiếp vào User để dễ quản lý khi nhóm đông thành viên <br> - **Thực hành:** tạo IAM Group/User/Role, switch role <br>&emsp;+ Tạo Group `developers` gắn Policy quyền hạn chế (không dùng AdministratorAccess), tạo User cá nhân thuộc Group thay vì dùng chung root account <br>&emsp;+ Thử switch sang 1 Role test để hiểu cơ chế `sts:AssumeRole` <br> - Học VPC: Subnet/Route Table/Internet Gateway/NAT Gateway/Security Group/NACL <br>&emsp;+ Phân biệt Security Group (stateful, theo instance) và NACL (stateless, theo subnet) — quyết định dùng SG là chính, NACL chỉ khi cần chặn rộng theo subnet <br> - **Thực hành:** dựng một VPC riêng với đầy đủ các thành phần trên <br>&emsp;+ Tạo 1 public subnet (route ra Internet Gateway) và 1 private subnet (route qua NAT Gateway) <br>&emsp;+ Test kết nối: EC2 ở public subnet SSH được từ ngoài vào, EC2 ở private subnet chỉ ra internet được qua NAT chứ không nhận kết nối trực tiếp từ ngoài | 24/06/2026 | 24/06/2026 | [AWS IAM](https://000002.awsstudygroup.com/vi/) <br> [Amazon VPC](https://000003.awsstudygroup.com/vi/) |
| 5 | - Cả nhóm thảo luận, chốt đề tài **Smart Docs AI** và tech stack (ReactJS, Python, AWS) <br>&emsp;+ Cân nhắc giữa vài ý tưởng ban đầu (app quản lý task, chatbot hỗ trợ tài liệu...) — chọn RAG chatbot xử lý tài liệu vì bám sát xu hướng GenAI và tận dụng được Bedrock thay vì tự train model <br>&emsp;+ Chốt ReactJS (frontend cả nhóm đã quen) + Python/FastAPI (dễ tích hợp LangChain) + kiến trúc serverless AWS (Lambda/API Gateway) để tối ưu chi phí demo <br> - Phác thảo wireframe giao diện ban đầu <br>&emsp;+ Vẽ nhanh các màn hình chính (đăng nhập, upload tài liệu, khung chat) để thống nhất luồng UX cơ bản trước khi code | 25/06/2026 | 25/06/2026 | |
| 6 | - Code các thành phần frontend ban đầu cho Smart Docs AI <br>&emsp;+ Dựng project bằng Vite + React, tạo các component khung (Layout, Sidebar, ChatWindow) theo wireframe đã thống nhất <br> - Đẩy source code lên GitHub của nhóm <br>&emsp;+ Tạo repo chung, thống nhất quy tắc nhánh (mỗi người 1 branch riêng, tạo PR để review trước khi merge vào main) | 26/06/2026 | 26/06/2026 | Project Team GitHub Repository |
| 7 | - Học Amazon EC2 cơ bản: instance types, AMI, EBS <br>&emsp;+ Ghi chú sự khác biệt giữa họ instance T (burstable, rẻ, hợp demo) và M/C (ổn định hơn nhưng đắt) — chọn dùng free tier `t2.micro`/`t3.micro` cho các bài thực hành <br> - Tổng quan về AWS Cloud9 <br>&emsp;+ Mở thử 1 môi trường Cloud9 mẫu để hình dung cloud IDE hoạt động ra sao, dù dự án cuối cùng chọn code local + push GitHub thay vì Cloud9 | 27/06/2026 | 27/06/2026 | [AWS Cloud9](https://000049.awsstudygroup.com/vi/) |


### Kết quả đạt được tuần 1:

* Làm quen với các thành viên FCAJ và nắm được quy trình làm việc trong kỳ thực tập.
* Nắm vững kiến thức nền tảng AWS Cloud: hạ tầng toàn cầu (Region, AZ), các nhóm dịch vụ chính, công cụ quản lý (Console/CLI).
* Tạo thành công tài khoản AWS Free Tier, bật MFA, thiết lập AWS Budgets để kiểm soát chi phí.
* Hiểu cơ chế phân quyền IAM (User/Group/Role/Policy) và dựng được một VPC riêng có Subnet/Route Table/Internet Gateway/NAT Gateway/Security Group.
* Chốt đề tài dự án **Smart Docs AI**, thống nhất tech stack (ReactJS, Python, AWS) cùng cả nhóm.
* Hoàn thành khung giao diện frontend ban đầu và đẩy code lên GitHub của nhóm.
* Làm quen sơ bộ với Amazon EC2 (instance type, AMI, EBS) chuẩn bị cho tuần học tiếp theo.


