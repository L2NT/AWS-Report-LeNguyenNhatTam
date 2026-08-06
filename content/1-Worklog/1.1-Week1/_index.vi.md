---
title: "Nhật ký Tuần 1: Nghiên cứu tổng quan AWS Cloud & Lựa chọn đề tài"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Mục tiêu tuần 1:

* Kết nối, làm quen với các thành viên chương trình First Cloud AI Journey (FCAJ) và nắm vững quỹ trình làm việc trong kỳ thực tập.
* Nghiên cứu kiến thức nền tảng về AWS Cloud, hạ tầng toàn cầu và các công cụ quản lý cốt lõi.
* Thực hành bảo mật tài khoản (MFA), phân quyền IAM và hạ tầng mạng (VPC).
* Thảo luận nhóm, chốt đề tài **Smart Docs AI** và triển khai giao diện Frontend ban đầu.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Làm quen các thành viên FCAJ, đọc nội quy thực tập <br>&emsp;+ Nắm lịch làm việc theo tuần, quy trình báo cáo và deadline nộp Worklog hàng tuần <br> - Xem "First Cloud Journey Kick off 2024", hướng dẫn vẽ kiến trúc AWS bằng Draw.io và hướng dẫn làm Workshop <br>&emsp;+ Cài đặt công cụ Hugo, làm quen cách tổ chức thư mục và cú pháp Markdown để soạn thảo báo cáo Workshop <br> - Dựng khung Workshop report, cập nhật thông tin giới thiệu cá nhân <br>&emsp;+ Khởi tạo sườn báo cáo từ mẫu, cập nhật thông tin cá nhân và chạy thử thành công ở môi trường cục bộ trước khi đồng bộ lên GitHub | 22/06/2026 | 22/06/2026 | [Kick off](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) <br> [Hướng dẫn Draw.io](https://www.youtube.com/watch?v=l8isyDe-GwY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=2) <br> [Hướng dẫn Workshop](https://www.youtube.com/watch?v=mXRqgMr_97U&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=3) |
| 3 | - Học điện toán đám mây là gì, điều gì tạo nên sự khác biệt của AWS, hạ tầng toàn cầu AWS (Region/AZ/Edge Location), công cụ quản lý AWS (Console/CLI/SDK) <br>&emsp;+ Phân biệt Region/Availability Zone/Edge Location, hiểu vì sao AWS dùng multi-AZ để đảm bảo high availability <br>&emsp;+ So sánh Console (trực quan, học nhanh) với CLI (tự động hoá, cần cho script deploy sau này) và SDK (tích hợp vào code) — quyết định học CLI song song Console ngay từ đầu <br> - Tổng quan các nhóm dịch vụ AWS: Compute/Storage/Networking/Database <br>&emsp;+ Ghi chú dịch vụ tiêu biểu mỗi nhóm (EC2/Lambda, S3/EBS, VPC, RDS/DynamoDB) làm cơ sở chọn kiến trúc cho Smart Docs AI sau này <br> - **Thực hành:** tạo AWS Free Tier account, bật MFA, tạo AWS Budget <br>&emsp;+ Bật MFA bằng Google Authenticator ngay từ đầu để tránh mất quyền kiểm soát root account <br>&emsp;+ Tạo AWS Budget cảnh báo ở ngưỡng $5/tháng, phòng trường hợp quên tắt tài nguyên demo | 23/06/2026 | 23/06/2026 | [Khái niệm Cloud](https://www.youtube.com/watch?v=HxYZAK1coOI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=4) <br> [AWS Free Tier](https://000001.awsstudygroup.com/vi/) <br> [AWS Budgets](https://000007.awsstudygroup.com/vi/) |
| 4 | - Học IAM: khái niệm Group/User/Policy/Role <br>&emsp;+ Nắm nguyên tắc least privilege — Policy nên gắn vào Group/Role thay vì gắn trực tiếp vào User để dễ quản lý khi nhóm đông thành viên <br> - **Thực hành:** tạo IAM Group/User/Role, chuyển đổi Role (Switch Role) <br>&emsp;+ Tạo Group gắn Policy quyền hạn chế (không dùng AdministratorAccess), tạo User cá nhân thuộc Group thay vì dùng chung root account <br>&emsp;+ Thực hành chuyển đổi sang một Role thử nghiệm để hiểu cơ chế cấp quyền tạm thời giữa các Role <br> - Học VPC: Subnet/Route Table/Internet Gateway/NAT Gateway/Security Group/NACL <br>&emsp;+ Phân biệt Security Group (stateful, theo instance) và NACL (stateless, theo subnet) — quyết định dùng SG là chính, NACL chỉ khi cần chặn rộng theo subnet <br> - **Thực hành:** dựng một VPC riêng với đầy đủ các thành phần trên <br>&emsp;+ Tạo 1 public subnet (route ra Internet Gateway) và 1 private subnet (route qua NAT Gateway) <br>&emsp;+ Kiểm tra kết nối: EC2 ở public subnet SSH được từ ngoài vào, EC2 ở private subnet chỉ ra internet được qua NAT chứ không nhận kết nối trực tiếp từ ngoài | 24/06/2026 | 24/06/2026 | [AWS IAM](https://000002.awsstudygroup.com/vi/) <br> [Amazon VPC](https://000003.awsstudygroup.com/vi/) |
| 5 | - **Thảo luận nhóm:** chốt đề tài **Smart Docs AI** và bộ công nghệ (ReactJS, Python, AWS) <br>&emsp;+ Cân nhắc giữa một số ý tưởng ban đầu (ứng dụng quản lý công việc, chatbot hỗ trợ tài liệu...) — quyết định chọn RAG chatbot xử lý tài liệu vì bám sát xu hướng GenAI và tận dụng được Amazon Bedrock thay vì tự huấn luyện mô hình <br>&emsp;+ Thống nhất ReactJS (Frontend nhóm đã quen) + Python/FastAPI (dễ tích hợp LangChain) + kiến trúc Serverless AWS (Lambda/API Gateway) để tối ưu chi phí vận hành <br> - Phác thảo giao diện sơ bộ (Wireframe) ban đầu <br>&emsp;+ Dựng nhanh các màn hình chính (đăng nhập, tải tài liệu, khung trò chuyện) để thống nhất luồng trải nghiệm người dùng cơ bản trước khi code | 25/06/2026 | 25/06/2026 | |
| 6 | - Code các thành phần giao diện Frontend ban đầu cho Smart Docs AI <br>&emsp;+ Tạo dự án bằng ReactJS, làm các thành phần giao diện khung theo Wireframe đã thống nhất <br> - Đồng bộ mã nguồn lên kho lưu trữ GitHub của nhóm <br>&emsp;+ Tạo kho lưu trữ chung, thống nhất quy tắc quản lý nhánh (mỗi thành viên một nhánh riêng, tạo Pull Request để rà soát trước khi hợp nhất vào nhánh chính) | 26/06/2026 | 26/06/2026 | Kho lưu trữ GitHub dự án nhóm |
| 7 | - Nghiên cứu Amazon EC2 cơ bản: các loại instance, AMI, ổ đĩa EBS <br>&emsp;+ Phân biệt các họ instance (burstable giá rẻ phù hợp demo và họ hiệu năng cao ổn định hơn nhưng chi phí lớn), ưu tiên dùng gói Free Tier cho các bài thực hành <br> - Tổng quan về AWS Cloud9 <br>&emsp;+ Thực hành một môi trường Cloud9 mẫu để hình dung cloud IDE hoạt động ra sao, dù dự án cuối cùng chọn code ở máy cục bộ và đồng bộ qua GitHub | 27/06/2026 | 27/06/2026 | [AWS Cloud9](https://000049.awsstudygroup.com/vi/) |


### Kết quả đạt được tuần 1:

* Làm quen với các thành viên FCAJ và nắm được quy trình làm việc trong kỳ thực tập.
* Nắm vững kiến thức nền tảng AWS Cloud: hạ tầng toàn cầu (Region, AZ), các nhóm dịch vụ chính, công cụ quản lý (Console/CLI).
* Tạo thành công tài khoản AWS Free Tier, bật MFA, thiết lập AWS Budgets để kiểm soát chi phí.
* Hiểu cơ chế phân quyền IAM (User/Group/Role/Policy) và dựng được một VPC riêng có Subnet/Route Table/Internet Gateway/NAT Gateway/Security Group.
* Chốt đề tài dự án **Smart Docs AI**, thống nhất bộ công nghệ (ReactJS, Python, AWS) cùng cả nhóm.
* Hoàn thành khung giao diện Frontend ban đầu và đồng bộ mã nguồn lên GitHub của nhóm.
* Làm quen sơ bộ với Amazon EC2 (instance type, AMI, EBS) chuẩn bị cho tuần học tiếp theo.


