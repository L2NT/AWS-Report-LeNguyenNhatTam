---
title: "Event 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Cloud Architect x Meet Up

### Mục Đích Của Sự Kiện

- Tạo một không gian thoải mái để các cloud architect, kỹ sư và người đang học AWS trao đổi kinh nghiệm thực tế
- Giới thiệu AWS Security Agent và nhấn mạnh vì sao bảo mật ngày càng quan trọng trong thời buổi "vibe code"
- Chia sẻ mẹo và tâm lý thi các chứng chỉ AWS
- Kết nối cộng đồng AWS Study Group / cloud qua những buổi gặp gỡ thân mật

### Danh Sách Diễn Giả

- **Anh Long** – Security Solutions Architect, showcase **AWS Security Agent** (một service chính thức của AWS) và chia sẻ vì sao bảo mật hệ thống lại rất quan trọng ở thời điểm hiện tại
- **Anh Huy** – AWS Certified Solutions Architect, chia sẻ kinh nghiệm thi chứng chỉ từ hành trình của chính anh

### Nội Dung Nổi Bật

#### Showcase AWS Security Agent (Anh Long)
- AWS Security Agent quét toàn bộ project từ đầu đến cuối, phát hiện nhiều loại lỗ hổng hơn hẳn lỗi cấu hình account thông thường — như secret/API key bị hardcode trong code, dependency lỗi thời có CVE đã biết, S3 bucket bị public hay security group mở quá rộng, thiếu mã hoá dữ liệu khi lưu trữ/truyền tải, và cả các lỗi ở tầng code như injection — rồi thể hiện toàn bộ kết quả qua giao diện trực quan (dashboard) thay vì log thô.
- Agent còn tự động xuất ra một báo cáo PDF đầy đủ, giúp team có ngay tài liệu để chia sẻ/xử lý mà không cần tự tổng hợp lại kết quả quét.
- Điểm đáng nhớ nhất: trong thời buổi "vibe code" — khi code được AI tạo ra hoặc copy-paste mà không ai đọc kỹ — lỗ hổng bảo mật rất dễ lọt vào hệ thống, nên việc có công cụ luôn để mắt đến bảo mật càng quan trọng hơn.

#### Mẹo thi chứng chỉ AWS (Anh Huy)
- Đề thi hoàn toàn là trắc nghiệm theo tình huống — không phải code, nhưng phải suy luận xem dịch vụ AWS nào thực sự phù hợp với tình huống được nêu.
- Mẹo khá đời thường nhưng hữu ích: phòng thi thường rất lạnh, nên mang theo áo khoác nếu không muốn bị phân tâm giữa chừng.
- Anh cũng chia sẻ về cách quản lý thời gian làm bài: nếu một câu mất quá nhiều thời gian mà vẫn chưa ra thì nên bỏ qua làm câu tiếp theo trước — đôi khi các câu phía sau lại vô tình gợi ý (thậm chí lộ luôn) đáp án cho câu trước đó. Giao diện bài thi có sẵn tính năng đánh flag để đánh dấu những câu chưa chắc, rồi quay lại xem toàn bộ các câu đã đánh flag sau khi làm hết bài.
- Anh cũng chia sẻ thêm là không phải câu nào cũng là trắc nghiệm 1 đáp án đúng như bình thường — có dạng câu "multiple response", yêu cầu chọn từ 2 đáp án đúng trở lên trong số 5 lựa chọn trở lên, nên cần để ý kỹ đề bài yêu cầu chọn bao nhiêu đáp án trước khi nộp.

### Những Gì Học Được

- Bảo mật không thể "để sau" khi rất nhiều code hiện nay được viết theo kiểu "vibe code" thay vì tự tay review từng dòng — lỗ hổng có thể ẩn ở bất cứ đâu, từ secret bị hardcode đến dependency lỗi thời, chứ không chỉ là lỗi cấu hình account.
- Một service chính thức như AWS Security Agent thật sự hữu ích để bắt những lỗi mà không ai kiểm tra thủ công, và việc đóng gói kết quả thành dashboard cùng báo cáo PDF tự động giúp dễ hành động hơn nhiều.
- Ôn thi chứng chỉ cũng cần chiến lược làm bài — biết khi nào nên bỏ qua và đánh flag câu khó, để ý dạng câu multiple response — chứ không chỉ là nắm vững kiến thức dịch vụ, và những buổi meetup nhỏ như thế này dễ đặt câu hỏi hơn hẳn hội thảo lớn.

### Ứng Dụng Vào Công Việc

- Thêm KMS cho DynamoDB (trước đó chưa có customer-managed key) và biến key này thành một deployment variable để dễ đổi theo từng môi trường.
- Thêm bước pytest chạy ở `pre_build` trong CodePipeline, để test chặn mọi bản build trước khi lên production — một lớp bảo mật mà trước đây chưa hề có.

### Trải nghiệm trong event

Đây là một buổi meetup nhỏ, thân mật vào buổi sáng chứ không phải hội thảo lớn, nên nội dung chia sẻ khá gần gũi và dễ tiếp thu. Mình chủ yếu ngồi nghe cả hai phần chia sẻ — phần của anh Long giúp mình hiểu rõ hơn AWS Security Agent quét được những loại lỗ hổng nào và báo cáo PDF tự động đó hữu ích ra sao, còn mẹo thi của anh Huy — nhất là chiến lược đánh flag và lưu ý về dạng câu multiple response — là kinh nghiệm thực tế mà tài liệu chính thức không ghi. Mình rời buổi đó với vài việc cụ thể cần kiểm tra lại trong hệ thống.

#### Một số hình ảnh khi tham gia sự kiện
*Ảnh sẽ được đặt trong `static/images/4-EventParticipated/4.1-Event1/` — sau khi thêm ảnh, chèn vào đây theo dạng `![](/images/4-EventParticipated/4.1-Event1/ten-anh.jpg)`.*
