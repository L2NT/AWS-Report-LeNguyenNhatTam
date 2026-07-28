---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# COLD START TRONG SERVERLESS: LÝ DO CHATBOT CỦA MÌNH THỈNH THOẢNG TRẢ LỜI KHÔNG THÀNH CÔNG

## Giới thiệu

Chào mọi người, nhóm mình đang làm một dự án chatbot hỏi-đáp tài liệu (RAG), chạy hoàn toàn serverless: API Gateway + Lambda (Docker container) cho backend, Amazon Bedrock cho LLM/Embeddings, FAISS cho tìm kiếm vector. Hệ thống hỗ trợ 3 chế độ RAG: Standard, Self-RAG, và Co-RAG (dùng 3 agent song song: Semantic FAISS, Keyword BM25, Conceptual LLM).

Khi build chế độ Co-RAG, mình gặp một hiện tượng khó chịu: cùng một câu hỏi, cùng một tài liệu, có lúc trả lời trong 5 giây, có lúc trả về lỗi `503 Service Unavailable` sau đúng 30 giây. Không phải lỗi logic, không phải bug code — mà là một đặc tính cố hữu của kiến trúc serverless: cold start.

Bài viết này giải thích cold start hoạt động thế nào (dựa theo loạt bài "Operating Lambda: Performance optimization" của AWS), số liệu đo thật mình thu thập được, và quan trọng nhất — tại sao mình chưa vội bật Provisioned Concurrency dù đó là giải pháp được AWS khuyến nghị.

## Cold start là gì?

Khi Lambda nhận một request, nếu không có execution environment nào đang "ấm" sẵn sàng, service phải:

1. Tải code function (từ S3 hoặc ECR nếu dùng container image)
2. Khởi tạo environment với memory/runtime/config đã cấu hình
3. Chạy code khởi tạo (initialization code) nằm ngoài handler
4. Cuối cùng mới chạy handler thực sự

Toàn bộ quá trình 1-3 gọi là cold start, có thể mất từ dưới 100ms đến hơn 1 giây cho function thông thường — nhưng với dự án của mình, function là 1 Docker image nặng (FastAPI + LangChain + FAISS + nhiều dependency AI), cộng thêm phải tải lại FAISS index của user từ S3, nên cold start thực tế nặng hơn nhiều.

Sau khi handler chạy xong, Lambda giữ lại execution environment trong một khoảng thời gian không xác định để tái sử dụng cho request tiếp theo — gọi là warm start, nhanh hơn hẳn vì bỏ qua toàn bộ bước 1-3.

## Vấn đề thật: Cold start cộng dồn với giới hạn cứng của API Gateway

Điều nhiều người (kể cả mình lúc đầu) hay nhầm lẫn: Lambda timeout mình cấu hình là 300 giây (5 phút) — quá dài để tự nó gây ra lỗi. Vấn đề thật nằm ở API Gateway, vốn có giới hạn cứng 29-30 giây cho integration timeout, đây là giới hạn nền tảng của AWS, không thể tăng, không phụ thuộc vào cấu hình Lambda.

Khi cold start xảy ra:
- Download Docker image: ~5-8s
- Load FAISS index của user từ S3: ~8-12s
- Khởi tạo kết nối Bedrock: ~3-5s
- Xử lý Co-RAG thật (3 agent song song, vốn là mode chậm nhất): ~5-10s

Cộng dồn lại dễ dàng vượt ngưỡng 30 giây → bị API Gateway cắt ngang, trả về `503`.

## Số liệu đo thật

Mình đã test trực tiếp trên production khi soạn screenshot cho phần kiểm thử hệ thống:

- Lần 1 (Lambda cold sau khi nguội): ~30s — lỗi 503
- Lần 2 (độc lập, cũng cold): ~30s — lỗi 503
- Lần 3 (ngay sau lần 2, Lambda đã warm): 9.53s — thành công
- Lần 4 (ngay sau lần 3): 4.44s — thành công
- Lần 5 (ngay sau lần 4): 9.02s — thành công

Ban đầu mình tưởng "Co-RAG luôn fail sau 30s" — chỉ vì 2 lần thử đầu tiên tình cờ đều rơi vào cold start. Test lại kỹ hơn mới thấy: khi Lambda đã ấm, Co-RAG chạy rất nhanh, thậm chí nhanh hơn cả Standard RAG (31.2s ở lần đo cold đầu tiên).

## Vì sao mình chưa bật Provisioned Concurrency ngay?

AWS khuyến nghị Provisioned Concurrency là giải pháp chuẩn để loại bỏ cold start — Lambda giữ sẵn N execution environment đã khởi tạo xong, sẵn sàng phản hồi ngay. Nhưng mình cân nhắc kỹ trước khi áp dụng:

1. **Chi phí luôn phát sinh dù không có traffic** — Provisioned Concurrency tính phí theo giờ cho mỗi environment được giữ sẵn, bất kể có request hay không. Với quy mô demo/thực tập (vài chục request/ngày), chi phí này không tương xứng lợi ích.
2. **Tần suất gặp cold start thực tế thấp** — cold start chỉ xảy ra ở lần gọi đầu tiên sau một khoảng "nguội", không phải mọi lần gọi.
3. **Đã có cơ chế retry ở frontend** — phiên bản frontend của mình có sẵn response interceptor tự động retry tối đa 10 lần, mỗi lần cách nhau 5 giây khi gặp lỗi 503/504. Với cold start là nguyên nhân duy nhất, user vẫn nhận được câu trả lời sau khoảng 40-45 giây (30s timeout đầu + 5s chờ retry + 5-10s lần gọi thứ 2 đã ấm) — chấp nhận được, dù chưa lý tưởng, ở quy mô hiện tại.
4. **Có phương án rẻ hơn nếu cần**: dùng EventBridge Rule gọi "ping" Lambda mỗi vài phút để giữ ấm — chi phí thấp hơn nhiều so với Provisioned Concurrency, dù không đảm bảo 100% (vẫn có thể cold start khi traffic scale lên, tạo nhiều execution environment mới cùng lúc).

Nói cách khác: đây không phải "bỏ qua best practice" mà là một quyết định có cân nhắc trade-off giữa chi phí và trải nghiệm người dùng, phù hợp với quy mô hiện tại của dự án — và sẽ được ưu tiên bật Provisioned Concurrency hoặc warm-up ping ngay khi traffic thực tế tăng lên.

## Kết luận

Cold start không phải là bug, mà là đặc tính cố hữu của kiến trúc serverless. Vấn đề chỉ thực sự nghiêm trọng khi cộng dồn với giới hạn cứng khác trong hệ thống (ở đây là API Gateway 30s). Hiểu rõ execution environment lifecycle giúp mình đưa ra quyết định tối ưu đúng chỗ, đúng thời điểm — thay vì áp dụng mọi best practice ngay từ đầu mà không cân nhắc chi phí/lợi ích thực tế.

## Link bài viết
https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-1/

## Link bài đã đăng trong AWS Study Group
https://www.facebook.com/groups/awsstudygroupfcj/permalink/2226685044763122/

...Hướng dẫn...