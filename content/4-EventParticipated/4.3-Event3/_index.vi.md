---
title: "Event 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---

# Agent Forge – Deepdive Day 2

### Mục Đích Của Sự Kiện

- Hướng dẫn cách làm và triển khai hệ thống Agentic AI ở mức production-ready bằng Amazon Bedrock AgentCore
- Đi sâu vào 3 feature của Day 2 gồm Memory, Observability và Evaluations
- Giới thiệu các component mở rộng và kết hợp lý thuyết với hands-on để người tham dự tự cấu hình một agent cơ bản
- Kết nối các thành viên trong cộng đồng AWS Study Group đang tìm hiểu và làm dự án về Agentic AI

### Danh Sách Diễn Giả

- **Anh Nghĩa** và **anh Anh** – trình bày các nội dung về Amazon Bedrock AgentCore và hướng dẫn phần hands-on

### Nội Dung Nổi Bật

AgentCore có 6 feature chính: Runtime, Identity, Gateway được trình bày ở Day 1; Memory, Observability và Evaluations là nội dung trọng tâm của Day 2.

#### AgentCore Memory

- Memory giải quyết giới hạn context window bằng cách đưa lịch sử và thông tin cần ghi nhớ ra một lớp lưu trữ riêng, giúp agent phản hồi theo ngữ cảnh của từng user
- Short-term memory lưu raw message của cuộc hội thoại theo thời gian thực, còn long-term memory trích xuất insight và knowledge để sử dụng lại ở những lần tương tác sau
- Ví dụ trong buổi học là chatbot tư vấn giày có thể nhớ hãng, màu sắc và lựa chọn trước đó của user thay vì hỏi lại từ đầu

#### AgentCore Observability

- Observability dùng log, trace và metric theo chuẩn OpenTelemetry để theo dõi toàn bộ flow xử lý của agent
- Dashboard giúp kiểm tra latency, lượng token sử dụng, lỗi phát sinh và thiết lập alert khi hệ thống vượt ngưỡng
- Điểm chính của phần này là phải nhìn thấy agent đang xử lý ở bước nào thì mới debug được một hệ thống có nhiều model và tool kết nối với nhau

#### AgentCore Evaluations

- Evaluations dùng LLM-as-a-Judge để đo chất lượng phản hồi thay vì chỉ review theo cảm tính, với các tiêu chí có sẵn như Correctness
- Có thể chạy on-demand trong lúc develop hoặc online để theo dõi agent khi hệ thống đang hoạt động
- Kết quả evaluation giúp phát hiện phần phản hồi chưa tốt rồi điều chỉnh system prompt, tool hoặc dữ liệu đầu vào

#### Các Component Khác

- Registry quản lý và tái sử dụng tool/skill; Harness giúp khởi tạo agent từ 3 phần cơ bản gồm Model, System Prompt và Tools
- Policy kết hợp với IAM để giới hạn quyền theo nguyên tắc least privilege; Tools, Code Interpreter và Knowledge Base mở rộng khả năng xử lý cũng như kết nối dữ liệu cho agent
- Payments hỗ trợ flow thanh toán qua Stripe/Coinbase, còn Optimization có phần Red Teaming để kiểm tra và cải thiện hệ thống

#### Hands-on Lab

- Setup môi trường gồm Kiro IDE, AWS CLI, AgentCore CLI và CDK rồi deploy agent Hello World
- Chỉnh system prompt để chuyển agent cơ bản thành Return and Refund Assistant
- Thêm Memory với thời gian lưu 7 ngày để agent duy trì ngữ cảnh hội thoại

### Những Gì Học Được

- Agent cần một lớp Memory riêng để không phải đưa toàn bộ lịch sử vào context window ở mỗi request, đồng thời có thể cá nhân hóa phản hồi theo từng user
- Short-term memory phù hợp với raw message trong session hiện tại, còn long-term memory giữ lại insight cần dùng ở những lần trò chuyện sau
- Observability không chỉ là xem log; cần kết hợp trace và metric để biết agent chậm hoặc lỗi ở model, tool hay hạ tầng
- Chất lượng phản hồi nên được đo bằng Evaluations theo tiêu chí cụ thể và chạy lại sau mỗi lần chỉnh prompt hoặc tool, thay vì chỉ đọc vài câu trả lời rồi tự đánh giá
- Phần AI core chỉ là một phần nhỏ của hệ thống; phần lớn công việc vẫn nằm ở software engineering như thêm tool, quản lý memory, phân quyền, theo dõi và tối ưu agent

### Ứng Dụng Vào Công Việc

- Cân nhắc dùng Memory cho RAG chatbot để giữ ngữ cảnh xuyên suốt nhiều lượt hỏi-đáp, thay vì xử lý mỗi câu hỏi như một request độc lập
- Tìm hiểu cách tách short-term và long-term memory để chỉ lưu những insight cần thiết, tránh đưa toàn bộ lịch sử chat vào prompt
- Có thể dùng Observability để theo dõi latency, token và lỗi trong RAG flow; dùng Evaluations để đo Correctness sau mỗi lần thay đổi prompt hoặc cách retrieval

### Trải nghiệm trong event

Tôi tham gia trực tiếp Day 2 nhưng không có mặt ở Day 1, nên bị thiếu phần setup ban đầu. Trong lúc mọi người làm hands-on, tôi chủ yếu cài AgentCore CLI và CDK, chỉ hoàn tất bước chuẩn bị môi trường chứ chưa chạy được các bài lab. Tôi dự định xem lại video Day 1 trên YouTube rồi làm lại từ đầu để theo kịp flow của workshop. Phần tôi ấn tượng nhất là Memory vì khá sát với vấn đề giữ ngữ cảnh hội thoại trong RAG chatbot của project.

#### Một số hình ảnh khi tham gia sự kiện
![Ảnh sự kiện 3](/images/4-EventParticipated/4.3-Event3/Event-08-08-2026.png)