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

### Blog 2 — [Kiến Trúc Bedrock AWS Landing Zone](3.2-Blog2/)
*Bài viết do bạn Phong trong nhóm thực hiện, được tính vào số lượng bài blog chung của nhóm theo quy định của chương trình FCAJ.* Phân tích baseline architecture khi triển khai Amazon Bedrock trong AWS Landing Zone: bảo mật kết nối mạng qua PrivateLink & VPC Lattice, quản lý định danh tập trung theo nguyên tắc least-privilege, và quản trị tập trung bằng Service Control Policies (SCPs) cùng audit trail qua CloudTrail.

### Blog 3 — [Lambda Tenant Isolation Mode: tính năng mới có giải quyết được bug rò rỉ dữ liệu multi-tenant không?](3.3-Blog3/)
Phân tích tính năng Lambda Tenant Isolation Mode (11/2025) trong bối cảnh bug rò rỉ dữ liệu giữa các user đã tự debug và fix thủ công trong dự án nhóm tôi làm — và vì sao tính năng cách ly compute-level mới này không thể thay thế việc thiết kế đúng data path theo từng tenant ở tầng ứng dụng.