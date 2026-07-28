---
title: "Các bài blogs đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice warning %}}  
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

Tại đây sẽ là phần liệt kê, giới thiệu các blogs mà các bạn đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Ví dụ:

###  [Blog 1 - EVENTBRIDGE SCHEDULER: KHI NÀO "NÂNG CẤP" KHỎI EVENTBRIDGE RULE?](3.1-Blog1/)
Amazon EventBridge Scheduler mạnh mẽ hơn nhiều so với EventBridge Rule truyền thống (1 triệu schedule, 270+ target, retry/DLQ, one-time schedule...). Bài viết liên hệ với việc dùng EventBridge Rule `rate(1 minute)` để dọn Cognito user chưa xác thực trong dự án nhóm mình làm, và phân tích vì sao Rule vẫn là lựa chọn hợp lý ở quy mô hiện tại thay vì vội chuyển sang Scheduler.

###  [Blog 2 - COLD START TRONG SERVERLESS: LÝ DO CHATBOT CỦA MÌNH THỈNH THOẢNG TRẢ LỜI KHÔNG THÀNH CÔNG](3.2-Blog2/)
Giải thích cơ chế cold start/warm start của AWS Lambda và vì sao nó cộng dồn với giới hạn cứng 30 giây của API Gateway gây lỗi 503. Kèm số liệu đo thật từ bug Co-RAG trong dự án nhóm mình làm, và lý do chưa vội bật Provisioned Concurrency dù đó là khuyến nghị chuẩn của AWS.

###  [Blog 3 - LAMBDA TENANT ISOLATION MODE: TÍNH NĂNG MỚI CÓ GIẢI QUYẾT ĐƯỢC BUG RÒ RỈ DỮ LIỆU MULTI-TENANT KHÔNG?](3.3-Blog3/)
Phân tích tính năng Lambda Tenant Isolation Mode (11/2025) trong bối cảnh bug rò rỉ dữ liệu giữa các user đã tự debug và fix thủ công trong dự án nhóm mình làm — và vì sao tính năng cách ly compute-level mới này không thể thay thế việc thiết kế đúng data path theo từng tenant ở tầng ứng dụng.