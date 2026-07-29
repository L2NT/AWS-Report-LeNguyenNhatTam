---
title: "Event 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Agentic AI Build Week powered by GenAI Fund

### Mục Đích Của Sự Kiện

- Tổng kết một hackathon quy mô lớn (FCAJ x Agentic AI Build Week) với nhiều đội thi (2K, Six Piller, One Team, Long & Co, và các đội khác)
- Tạo sân khấu để các đội demo và pitch sản phẩm Agentic AI xây dựng trên nền tảng AWS
- Chia sẻ những bài học "xương máu" từ 24 giờ làm hackathon — teamwork, kỹ năng pitching, và các câu chuyện kỹ thuật thực tế
- Giúp người tham gia có dự án đẹp cho hồ sơ (CV) và kết nối với cộng đồng AWS Study Group

### Danh Sách Diễn Giả

- **One Team** – làm chatbot đặt đồ ăn kiểu Zalo, tập trung vào giao diện hội thoại dễ dùng cho người không rành công nghệ
- **Long & Co** – làm trợ lý AI cho Solution Architect, biến yêu cầu ngôn ngữ tự nhiên thành sơ đồ kiến trúc, dự toán chi phí và IaC có thể deploy
- **Nhóm 2K** – làm hệ thống giám sát đám đông real-time bằng computer vision kết hợp agentic AI copilot
- **Six Piller** – làm Adaptive Workflow Engine hỗ trợ phân loại case phòng chống rửa tiền (AML)

### Nội Dung Nổi Bật

#### One Team – chatbot đặt đồ ăn qua hội thoại
- Bỏ qua việc làm hẳn một app phức tạp, chọn giao diện chat tối giản kiểu Zalo để người không rành công nghệ không phải học cách dùng app mới.
- Dùng prompt ngôn ngữ tự nhiên thay vì bấm chọn món, để AI tự suy luận ý định người dùng — không cần đăng ký tài khoản.
- Demo trên một bộ dữ liệu doanh nghiệp mô phỏng (kịch bản kiểu FPT) để cho thấy agent có thể truy vấn dữ liệu cấu trúc (mã số thuế, doanh thu theo quý) và đưa ra đề xuất.
- Bài học lớn nhất của nhóm: công nghệ dù xịn đến đâu cũng phải bị giới hạn bởi nghiệp vụ thực tế, và việc đưa MVP lên production sớm quan trọng hơn là chỉ dừng ở lý thuyết.

#### Long & Co – trợ lý AI cho Solution Architect
- Giải quyết đúng nỗi đau của SA: phải thiết kế kiến trúc, dự toán chi phí và triển khai hệ thống trong thời gian cực ngắn (có khi chỉ một buổi tối), trong khi vẽ tay trên Draw.io và viết IaC thủ công tốn rất nhiều thời gian.
- Luồng xử lý: yêu cầu bằng ngôn ngữ tự nhiên + tài liệu nội bộ → AI vẽ sơ đồ kiến trúc → tính chi phí AWS dự kiến → sinh code Terraform/CloudFormation → con người xem xét và duyệt → hệ thống tự động deploy.
- Cái khó theo nhóm chia sẻ không nằm ở việc vẽ sơ đồ, mà ở việc quản lý context/memory của AI để kiến trúc luôn nhất quán với quy tắc nội bộ (ví dụ: Lambda phải nằm trong VPC), và validate output theo danh sách dịch vụ được phép dùng ở mỗi lần chạy.
- Giữ phạm vi ở mức proof-of-concept có thể chứng minh được, với UI hiển thị từng bước để ban giám khảo theo dõi luồng suy luận của agent theo thời gian thực.

#### Nhóm 2K – giám sát đám đông real-time
- Pipeline: camera đẩy dữ liệu qua Amazon Kinesis Video Streams → container chạy trên AWS Fargate dùng YOLO để phát hiện người và ByteTrack để theo dõi (tránh đếm trùng hoặc bỏ sót) → dữ liệu mật độ lưu ở DynamoDB và S3.
- Lớp agentic AI (Bedrock + OpenAI) cho phép người vận hành hỏi hệ thống bằng ngôn ngữ tự nhiên để tóm tắt tình trạng khu vực hoặc đề xuất điều phối nhân sự.
- Tính năng nổi bật: người vận hành có thể tự vẽ các "zone" giám sát trên khung hình (cổng lên máy bay, hàng chờ thanh toán...), hệ thống sẽ cảnh báo đổi màu khi mật độ vượt ngưỡng.
- Khó khăn kỹ thuật lớn nhất là độ ổn định đường truyền cho xử lý video real-time, và cần camera đặt cố định ở góc cao để đếm zone chính xác.

#### Six Piller – Adaptive Workflow Engine chống rửa tiền
- Mục tiêu thay thế quy trình tra cứu thủ công tốn khoảng 20–25 USD và 3 giờ mỗi ca, dễ khiến chuyên viên phân tích bị "burn-out".
- Pipeline 3 lớp: Lớp 1 chấm điểm rủi ro (0–1) theo thời gian thực qua Kinesis Data Streams + XGBoost trên Amazon Bedrock; Lớp 2 dùng AWS Step Functions điều phối các agent chuyên trách (KYC, phân tích giao dịch, xây dựng bằng chứng) để tổng hợp file bằng chứng; Lớp 3 phân loại case thành Hold, Dismiss, hoặc Escalate cho con người xử lý.
- Triết lý thiết kế: AI là "cánh tay phải" chứ không thay thế con người do tính nhạy cảm của tài chính — toàn bộ logic suy luận và bằng chứng đều được ghi lại để phục vụ audit, và hệ thống giúp một chuyên viên xử lý được nhiều case hơn.

#### Bài học từ 24 giờ hackathon
- Teamwork quan trọng hơn từng dòng code — những đội chia vai trò rõ ràng (backend, frontend, research, presenter) và bỏ được cái tôi cá nhân thường làm nhanh hơn.
- Ban giám khảo hỏi nhiều trong lúc pitching thực ra là dấu hiệu tốt — chứng tỏ họ quan tâm; xoáy vào pain point thực tế của khách hàng thay vì chỉ khoe công nghệ giúp phần trình bày nổi bật hơn.
- Các câu chuyện thực tế gồm sự cố hạ tầng, lỡ push file `.env` lên GitHub, thiếu ngủ, và cuống cuồng xử lý khi mạng yếu ngay lúc demo trực tiếp.
- Lời nhắn của ban tổ chức: đừng quá đặt nặng chuyện thắng thua — giá trị thật nằm ở trải nghiệm (kết nối, học công nghệ mới, thử giới hạn bản thân), và các dự án này cũng là điểm cộng đẹp cho CV sau này.

### Những Gì Học Được

- Dù thuộc các lĩnh vực rất khác nhau (đặt đồ ăn, kiến trúc cloud, computer vision, AML), điểm chung là các đội đều xuất phát từ một pain point thực tế thay vì chạy theo công nghệ trước.
- Pattern agentic AI lặp lại nhiều lần: một lớp điều phối (như Step Functions) quản lý các agent chuyên trách, có bước con người duyệt (human-in-the-loop) trước khi làm gì rủi ro, và phải quản lý context/memory để output AI nhất quán.
- Một hackathon dạy về teamwork và áp lực thời gian không kém gì kỹ thuật — nhiều lời khuyên hay nhất lại đến từ phần "chia sẻ điều gì đã sai" hơn là từ chính phần demo.

### Ứng Dụng Vào Công Việc

- Cân nhắc thêm bước con người duyệt (human-in-the-loop) trước khi để AI tự thực hiện hành động ảnh hưởng đến hạ tầng hoặc ra quyết định tài chính/bảo mật, giống cách Long & Co và Six Piller thiết kế.
- Tìm hiểu pattern điều phối (như Step Functions) để quản lý nhiều agent chuyên trách thay vì làm một agent to ôm hết mọi việc.

### Trải nghiệm trong event

Đây là buổi tổng kết/demo day của một hackathon chứ không phải buổi chia sẻ kiểu hội thảo, nên gần như cả buổi là 4 đội pitch nối tiếp nhau, sau đó là phần chia sẻ mở về hành trình 24 giờ vừa qua. Mình chủ yếu ngồi xem phần demo và Q&A — ấn tượng nhất là hệ thống chống rửa tiền của Six Piller và trợ lý kiến trúc của Long & Co, vì cả hai đều thiết kế theo hướng con người vẫn duyệt lại trước khi hành động, thay vì để AI tự động hoàn toàn.

#### Một số hình ảnh khi tham gia sự kiện
![Ảnh sự kiện 2](/images/4-EventParticipated/4.2-Event2/Event-25-07-2026.png)
