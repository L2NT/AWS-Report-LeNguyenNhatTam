---
title: "Các bài blogs đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Đây là 3 bài blog kỹ thuật tôi đã viết và đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj), mỗi bài đều dựa trên 1 bài viết chính thức trên AWS Blog và liên hệ trực tiếp với những gì tôi đã tự tay triển khai/debug trong quá trình làm dự án.

### Blog 1 — [EventBridge Scheduler: khi nào "nâng cấp" khỏi EventBridge Rule?](3.1-Blog1/)
Amazon EventBridge Scheduler mạnh mẽ hơn nhiều so với EventBridge Rule truyền thống (1 triệu schedule, 270+ target, retry/DLQ, one-time schedule...). Bài viết liên hệ với việc dùng EventBridge Rule `rate(1 minute)` để dọn Cognito user chưa xác thực trong dự án nhóm tôi làm, và phân tích vì sao Rule vẫn là lựa chọn hợp lý ở quy mô hiện tại thay vì vội chuyển sang Scheduler.

### Blog 2 — [Cold start trong serverless: lý do chatbot của tôi thỉnh thoảng trả lời không thành công](3.2-Blog2/)
Giải thích cơ chế cold start/warm start của AWS Lambda và vì sao nó cộng dồn với giới hạn cứng 30 giây của API Gateway gây lỗi 503. Kèm số liệu đo thật từ bug Co-RAG trong dự án nhóm tôi làm, và lý do chưa vội bật Provisioned Concurrency dù đó là khuyến nghị chuẩn của AWS.

### Blog 3 — [Lambda Tenant Isolation Mode: tính năng mới có giải quyết được bug rò rỉ dữ liệu multi-tenant không?](3.3-Blog3/)
Phân tích tính năng Lambda Tenant Isolation Mode (11/2025) trong bối cảnh bug rò rỉ dữ liệu giữa các user đã tự debug và fix thủ công trong dự án nhóm tôi làm — và vì sao tính năng cách ly compute-level mới này không thể thay thế việc thiết kế đúng data path theo từng tenant ở tầng ứng dụng.