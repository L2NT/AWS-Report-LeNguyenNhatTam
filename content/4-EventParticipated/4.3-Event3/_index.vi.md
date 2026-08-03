---
title: "Event 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---

# Agent Forge – Deepdive Day 2

### Mục Đích Của Sự Kiện

- Đào sâu (deep-dive) vào Amazon Bedrock AgentCore ở mức nâng cao (L300), tập trung vào 3 mảng cốt lõi: Memory, Evaluations, Observability
- Giới thiệu đầy đủ các thành phần (components) của nền tảng AgentCore: Registry, Harness, Tools, Payments, Optimization, Policy
- Kết hợp lý thuyết với hands-on lab để người tham dự tự tay thực hành ngay trong buổi học
- Kết nối cộng đồng đang xây dựng agentic AI trên nền tảng AWS

### Nội Dung Buổi Học

- **AgentCore L300**: đi sâu vào 3 module cốt lõi — Memory (agent ghi nhớ ngữ cảnh/lịch sử tương tác qua nhiều phiên), Evaluations (đo lường chất lượng phản hồi của agent một cách có hệ thống), Observability (theo dõi, debug hành vi agent theo thời gian thực)
- **AgentCore Components**: tổng quan 6 thành phần chính của nền tảng — Registry (đăng ký/quản lý agent), Harness (khung chạy agent), Tools (tích hợp tool calling), Payments (xử lý giao dịch trong agent), Optimization (tối ưu hiệu năng/chi phí), Policy (quản lý quyền hạn và ràng buộc hành vi agent)

### Hands-on Lab

- Thêm memory để agent phản hồi mang tính cá nhân hóa hơn theo từng user
- Khám phá Agent Observability để theo dõi hành vi agent
- Dùng AgentCore Evaluations để đo lường hiệu năng agent
- Khám phá AgentCore Harness

### Kỳ Vọng Áp Dụng Vào Dự Án

- Cân nhắc áp dụng cơ chế Memory của AgentCore cho phần RAG chatbot của dự án, để agent ghi nhớ được ngữ cảnh hội thoại xuyên suốt nhiều lượt hỏi-đáp thay vì xử lý từng câu hỏi độc lập.
- Tìm hiểu AgentCore Evaluations như một cách đo lường chất lượng câu trả lời có hệ thống hơn, thay vì chỉ test thủ công như hiện tại.
- Quan tâm đến Observability để debug rõ ràng hơn khi Co-RAG hoặc Self-RAG cho ra kết quả không như mong đợi.
