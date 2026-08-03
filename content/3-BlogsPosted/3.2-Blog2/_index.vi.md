---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# KIẾN TRÚC BEDROCK AWS LANDING ZONE

> *Bài viết dưới đây do bạn Phong trong nhóm thực hiện, được tính vào số lượng bài blog chung của cả nhóm (3 bài) theo quy định của chương trình FCAJ.*

![Sơ đồ kiến trúc Amazon Bedrock Baseline Architecture trong AWS Landing Zone](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/06/18/ARCHBLOG-1133-image-1-960x630.png)

### 1. Tổng Quan Kiến Trúc Nền Tảng (Baseline Architecture)
Khi triển khai ứng dụng Generative AI (GenAI) cấp doanh nghiệp với Amazon Bedrock, việc xây dựng một hạ tầng chuẩn mực (baseline architecture) nằm trong môi trường AWS Landing Zone (quản lý qua AWS Control Tower) là yêu cầu tiên quyết để đảm bảo tính an toàn, sẵn sàng cao và tuân thủ chính sách quản trị dữ liệu.

Mô hình Landing Zone chia tách hạ tầng doanh nghiệp thành các tài khoản AWS chuyên biệt (Multi-Account Strategy):
* **Core Network Account:** Quản lý các kết nối mạng tập trung và VPC Endpoints.
* **Security & Governance Account:** Quản lý nhật ký truy vết CloudTrail và kiểm soát tuân thủ.
* **Workload/AI Application Account:** Chứa ứng dụng xử lý và dịch vụ Amazon Bedrock.

---

### 2. Bảo Mật Kết Nối Mạng Chiều Sâu Với AWS PrivateLink & VPC Lattice
Hệ thống loại bỏ hoàn toàn việc lưu thông lưu lượng dữ liệu GenAI qua Internet bằng cách áp dụng các điểm truy cập riêng tư:
* **Amazon Bedrock VPC Endpoints (AWS PrivateLink):** Cho phép các máy chủ và ứng dụng trong VPC nội bộ gửi yêu cầu gọi mô hình nền (Foundation Models) hoặc Knowledge Base trực tiếp qua mạng nội bộ AWS, không đi qua cổng Internet công khai.
* **Amazon VPC Lattice Auth Policies:** Áp dụng chính sách xác thực và ủy quyền IAM ở cấp độ dịch vụ mạng (Network Level), đảm bảo chỉ những microservices hợp lệ mới được phép giao tiếp với Bedrock API.

---

### 3. Quản Lý Định Danh Tập Trung & Phân Quyền Giới Hạn (Least Privilege)
* **AWS IAM Identity Center (SSO):** Kết nối với hệ thống quản lý người dùng doanh nghiệp (Active Directory/Okta) để cấp quyền truy cập SSO an toàn cho đội ngũ phát triển và các ứng dụng tiêu thụ API.
* **IAM Resource Policies & KMS Encryption:** Tất cả tài nguyên Amazon Bedrock (Knowledge Base, Custom Models, Fine-tuning datasets) đều được mã hóa bằng chìa khóa AWS KMS do khách hàng quản lý (KMS CMK) và bảo vệ bằng IAM Resource Policies khắt khe.

---

### 4. Quản Trị Tập Trung Với Service Control Policies (SCPs) & Audit Trail
* **Service Control Policies (SCPs):** Ngăn chặn người dùng hoặc ứng dụng tạo tài nguyên Bedrock ở các AWS Region không được phép, hoặc vô hiệu hóa các tính năng ghi log bắt buộc.
* **Giám sát & Ghi vết toàn diện:** Mọi hành vi gọi mô hình Bedrock, cập nhật Knowledge Base hoặc truy cập dữ liệu đều được ghi lại đầy đủ vào AWS CloudTrail và CloudWatch Logs, phục vụ công tác đánh giá an ninh định kỳ.

---

### Tài Liệu Tham Khảo
* **Link blog:** [https://www.facebook.com/groups/awsstudygroupfcj/permalink/2207763766655250](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2207763766655250)
* **Bài viết gốc trên AWS Architecture Blog:** [Amazon Bedrock baseline architecture in an AWS landing zone](https://aws.amazon.com/vi/blogs/architecture/amazon-bedrock-baseline-architecture-in-an-aws-landing-zone/)
