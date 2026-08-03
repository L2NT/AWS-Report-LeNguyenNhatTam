---
title: "Mẫu 9 - Hướng dẫn trình bày báo cáo thực tập tốt nghiệp"
date: 2024-01-01
weight: 19
chapter: false
pre: " <b> 19. </b> "
---

# MỤC LỤC

- NHẬN XÉT CỦA CHUYÊN GIA HƯỚNG DẪN ..................................................... 3
- NHẬN XÉT CỦA GIẢNG VIÊN HƯỚNG DẪN ..................................................... 4
- LỜI MỞ ĐẦU ..................................................................................................... 5
- CHƯƠNG 1. GIỚI THIỆU .................................................................................. 6
  - 1.1. Giới thiệu công ty thực tập .......................................................................... 6
  - 1.2. Nhiệm vụ thực tập ........................................................................................ 6
- CHƯƠNG 2. NỘI DUNG THỰC TẬP .................................................................. 7
- CHƯƠNG 3. KẾT QUẢ THỰC TẬP ................................................................... 8
- CHƯƠNG 4. KẾT LUẬN VÀ KIẾN NGHỊ ......................................................... 12
- TÀI LIỆU THAM KHẢO ..................................................................................... 13
- PHỤ LỤC 1 ........................................................................................................... 14
- PHỤ LỤC 2 ........................................................................................................... 15
- PHỤ LỤC 3 ........................................................................................................... 16

# NHẬN XÉT CỦA CHUYÊN GIA DOANH NGHIỆP

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

# NHẬN XÉT CỦA GIẢNG VIÊN HƯỚNG DẪN

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

....................................................................................................................................

# LỜI MỞ ĐẦU

Cuộc cách mạng công nghệ 4.0 cùng sự bùng nổ của trí tuệ nhân tạo tạo sinh (Generative AI) đang thay đổi cách các doanh nghiệp lưu trữ, tìm kiếm và khai thác tri thức từ khối lượng tài liệu khổng lồ. Nhận thấy đây là một lĩnh vực có tính ứng dụng cao và phù hợp với định hướng phát triển bản thân, em đã lựa chọn tham gia chương trình thực tập **First Cloud AI Journey (FCAJ)** do Công ty TNHH Amazon Web Services Việt Nam tổ chức, với mong muốn được tiếp cận thực tế các dịch vụ điện toán đám mây AWS và mô hình AI tạo sinh (Amazon Bedrock) thông qua một dự án cụ thể.

Trong suốt quá trình thực tập, em cùng nhóm đã trực tiếp tham gia xây dựng dự án **SmartDocAI** — nền tảng hỏi đáp và trích xuất tri thức tài liệu thông minh trên nền tảng AWS Serverless, từ giai đoạn tìm hiểu yêu cầu, thiết kế kiến trúc, triển khai hạ tầng cho đến kiểm thử và vận hành.

Báo cáo này trình bày lại toàn bộ quá trình thực tập của em, bao gồm: giới thiệu về đơn vị thực tập và chương trình FCAJ, nhiệm vụ được giao, nội dung công việc đã thực hiện, kết quả đạt được qua từng tuần, cùng những bài học kinh nghiệm và kiến nghị rút ra sau đợt thực tập.

Em xin chân thành cảm ơn chuyên gia hướng dẫn tại doanh nghiệp — anh Nguyễn Gia Hưng, cùng giảng viên hướng dẫn tại Trường Đại học Sài Gòn đã tận tình hỗ trợ em trong suốt quá trình thực tập.

# CHƯƠNG 1. GIỚI THIỆU

## 1.1. Giới thiệu công ty thực tập

- **Tên công ty:** Công ty TNHH Amazon Web Services Việt Nam
- **Địa chỉ:** ....................................................
- **Lĩnh vực hoạt động:** Điện toán đám mây (Cloud Computing) — Amazon Web Services (AWS) là nhà cung cấp dịch vụ điện toán đám mây hàng đầu thế giới, thuộc tập đoàn Amazon, cung cấp hơn 200 dịch vụ trên phạm vi toàn cầu bao gồm Compute, Storage, Database, Networking, AI/Machine Learning,...
- **Vị trí thực tập:** Workforce Bootcamp - First Cloud AI Journey
- **Chuyên gia doanh nghiệp hướng dẫn trực tiếp:** Anh Nguyễn Gia Hưng

**Về chương trình First Cloud AI Journey (FCAJ):**

First Cloud AI Journey là chương trình thực tập/đào tạo (Workforce Bootcamp) do Amazon Web Services Việt Nam tổ chức dành cho sinh viên năm cuối các ngành Công nghệ thông tin, nhằm trang bị kiến thức nền tảng về điện toán đám mây AWS và trí tuệ nhân tạo tạo sinh (Generative AI) thông qua mô hình "học đi đôi với hành" (learning by doing). Sinh viên tham gia không chỉ được đào tạo lý thuyết mà còn trực tiếp tham gia xây dựng, triển khai một dự án thực tế trên hạ tầng AWS dưới sự hướng dẫn sát sao của các chuyên gia (mentor) của AWS xuyên suốt toàn bộ đợt thực tập.

Trong quá trình tham gia FCAJ, các nhóm sinh viên được:

- Tự đề xuất và bảo vệ ý tưởng dự án (Bản đề xuất — Mẫu 2) trước khi bắt tay vào triển khai.
- Được mentor của AWS hỗ trợ định kỳ hàng tuần để review kiến trúc, code, tiến độ dự án.
- Tham gia các buổi workshop/sự kiện chia sẻ kiến thức chuyên sâu về các dịch vụ AWS do đội ngũ Solutions Architect của AWS tổ chức.
- Ghi nhận kết quả thực tập hàng tuần (Mẫu 6) có xác nhận của chuyên gia hướng dẫn.

Em được phân công thực tập theo mô hình nhóm 3 sinh viên (cùng 2 bạn Phong và Trọng), cùng triển khai chung dự án SmartDocAI, trong đó em đảm nhiệm phần trọng tâm về Backend, bảo mật hệ thống (multi-tenancy, CSRF, KMS) và biên soạn tài liệu kỹ thuật/workshop.

## 1.2. Nhiệm vụ thực tập

Theo phân công của chuyên gia doanh nghiệp hướng dẫn (anh Nguyễn Gia Hưng) và đề cương học phần thực tập tốt nghiệp, nhóm 3 sinh viên (Tâm, Phong, Trọng) được giao nhiệm vụ nghiên cứu, thiết kế và triển khai hoàn chỉnh dự án **SmartDocAI** — nền tảng hỏi đáp & trích xuất tri thức tài liệu thông minh trên AWS Serverless (chi tiết xem [Bản đề xuất](https://l2nt.github.io/AWS-Report-LeNguyenNhatTam/vi/2-proposal/) — Mẫu 2), cụ thể:

- Tìm hiểu và thực hành các dịch vụ AWS nền tảng: IAM, VPC, EC2, S3, RDS/Aurora, DynamoDB, Lambda, API Gateway, CloudFront, Cognito, Bedrock, CodePipeline/CodeBuild, CloudWatch, KMS, EventBridge.
- Thiết kế kiến trúc Serverless Container Architecture (FastAPI trên Lambda + React SPA) và triển khai từng thành phần hạ tầng.
- Xây dựng luồng xác thực người dùng (Cognito, JWT, Google OAuth) và cơ chế bảo mật/phân lập dữ liệu đa người dùng (multi-tenancy).
- Xây dựng pipeline RAG (Retrieval-Augmented Generation) hỏi đáp tài liệu tích hợp Amazon Bedrock.
- Tự động hóa CI/CD với AWS CodePipeline/CodeBuild, thiết lập giám sát (CloudWatch Alarms/SNS) và các cơ chế production-hardening (mã hóa KMS, S3 Intelligent-Tiering, EventBridge cleanup, CSRF protection).
- Biên soạn tài liệu workshop hướng dẫn triển khai lại toàn bộ hệ thống (Chương 5) phục vụ cộng đồng học tập.

Riêng cá nhân em tập trung chính vào mảng Backend (FastAPI, Lambda), bảo mật hệ thống và biên soạn tài liệu kỹ thuật/workshop, trong khi 2 bạn cùng nhóm phụ trách các mảng Backend khác (Phong) và Frontend (Trọng).

### Kết luận chương 1

Chương 1 đã giới thiệu tổng quan về Công ty TNHH Amazon Web Services Việt Nam, chương trình thực tập First Cloud AI Journey và nhiệm vụ thực tập được giao. Các chương tiếp theo sẽ trình bày chi tiết nội dung công việc đã thực hiện và kết quả đạt được trong suốt đợt thực tập.

# CHƯƠNG 2. NỘI DUNG THỰC TẬP

Trong suốt đợt thực tập, nhóm đã triển khai dự án **SmartDocAI** theo kiến trúc Serverless hoàn toàn trên nền tảng AWS, gồm các thành phần chính: Frontend (React SPA lưu trữ trên S3, phân phối qua CloudFront), Backend (FastAPI đóng gói Docker chạy trên AWS Lambda, expose qua API Gateway), xác thực người dùng qua AWS Cognito, lưu trữ dữ liệu (Amazon S3, DynamoDB) và mô hình AI tạo sinh Amazon Bedrock (Titan Embeddings V2, Qwen 3 Next 80B) phục vụ pipeline RAG (Retrieval-Augmented Generation) hỏi đáp tài liệu. Mục tiêu, vấn đề cần giải quyết và sơ đồ kiến trúc chi tiết của dự án đã được trình bày tại [Bản đề xuất](https://l2nt.github.io/AWS-Report-LeNguyenNhatTam/vi/2-proposal/) (Mẫu 2).

Cá nhân em đảm nhiệm chính các nội dung sau:

**a. Xây dựng và bảo mật luồng xác thực người dùng**

- Kiểm thử toàn bộ luồng xác thực (đăng ký, xác nhận OTP, đăng nhập, Google Sign-In) tích hợp AWS Cognito.
- Phát hiện và khắc phục lỗi rò rỉ dữ liệu giữa các người dùng (multi-tenancy bug) trong luồng truy vấn tài liệu/RAG.
- Triển khai cơ chế bảo vệ chống tấn công CSRF cho luồng OAuth (state UUID parameter).

**b. Vận hành, giám sát và tối ưu chi phí hạ tầng**

- Cấu hình CloudWatch Alarms & SNS Alerting để giám sát tình trạng hệ thống theo thời gian thực.
- Áp dụng S3 Intelligent-Tiering để tối ưu chi phí lưu trữ tài liệu người dùng.
- Cấu hình mã hóa dữ liệu at-rest trên DynamoDB bằng AWS KMS.
- Xây dựng cơ chế tự động dọn dẹp tài khoản chưa xác thực bằng AWS EventBridge.

**c. Kiểm thử tự động & tích hợp CI/CD**

- Viết bộ kiểm thử tự động (pytest, khoảng 60 test case) cho các API Backend, tích hợp vào AWS CodePipeline theo cơ chế hard-fail (build thất bại nếu test không đạt).

**d. Biên soạn tài liệu kỹ thuật & Workshop**

- Vẽ và cập nhật các sơ đồ kiến trúc hệ thống (Frontend, Backend, CI/CD Pipeline, Cleanup Flow) bằng draw.io.
- Biên soạn chi tiết tài liệu hướng dẫn triển khai lại toàn bộ hệ thống từ đầu, trình bày tại [Chương 5 — Workshop](https://l2nt.github.io/AWS-Report-LeNguyenNhatTam/vi/5-workshop/) của báo cáo này, bao gồm các bước chuẩn bị môi trường, triển khai Frontend/Backend, kiểm thử hệ thống và tổng kết chi phí.

Với mỗi nội dung trên, giải pháp áp dụng, khó khăn gặp phải và kết quả đạt được đều được ghi nhận chi tiết theo tuần tại Chương 3 và tại [Nhật ký thực tập (Worklog)](https://l2nt.github.io/AWS-Report-LeNguyenNhatTam/vi/1-worklog/) của trang báo cáo.

**Kết luận chương 2**

Chương 2 đã trình bày nội dung công việc thực tế đã thực hiện trong đợt thực tập, tập trung vào các mảng bảo mật xác thực, vận hành/giám sát hạ tầng, kiểm thử tự động và biên soạn tài liệu kỹ thuật. Chương tiếp theo sẽ trình bày cụ thể kết quả đạt được qua từng tuần.

# CHƯƠNG 3: KẾT QUẢ THỰC TẬP

Sau 6 tuần đầu thực tập (22/06/2026 – 01/08/2026), nhóm đã đạt được các kết quả cụ thể sau (chi tiết từng tuần xem tại [Mẫu 6](https://l2nt.github.io/AWS-Report-LeNguyenNhatTam/vi/16-mau6/) và [Worklog](https://l2nt.github.io/AWS-Report-LeNguyenNhatTam/vi/1-worklog/)):

- Hoàn thành toàn bộ hạ tầng Serverless: Cognito, API Gateway, Lambda (Docker), S3, DynamoDB, CloudFront, Bedrock.
- Hoàn thiện luồng xác thực người dùng (đăng ký/đăng nhập/Google OAuth) và phát hiện, khắc phục thành công lỗi bảo mật multi-tenancy nghiêm trọng trước khi lên production.
- Xây dựng thành công pipeline RAG 3 chế độ (Standard RAG/Self-RAG/Co-RAG) hỏi đáp tài liệu chính xác, có trích dẫn nguồn.
- Thiết lập đầy đủ cơ chế giám sát (CloudWatch/SNS), bảo mật dữ liệu (KMS), tối ưu chi phí (S3 Intelligent-Tiering) và tự động hóa CI/CD với pytest khoảng 60 test case.
- Hoàn thành 3 bài blog chia sẻ kiến thức và tài liệu Workshop hướng dẫn triển khai lại toàn bộ hệ thống.
- Tham gia các sự kiện chia sẻ kiến thức về AWS Security và Generative AI do AWS tổ chức.

*(các bảng thông tin tiếp theo là để minh họa)*

### BẢNG GHI NHẬN KẾT QUẢ THỰC TẬP HÀNG TUẦN

Sinh viên có thể trình bày chi tiết hơn các công việc đã làm trong mỗi tuần (Mẫu 6). Cuối phần này đính kèm bảng ghi nhận kết quả thực tập hàng tuần có chữ ký của chuyên gia hướng dẫn.

### BẢNG ĐÁNH GIÁ QUÁ TRÌNH THỰC TẬP TỐT NGHIỆP

*(Do chuyên gia doanh nghiệp đánh giá — Mẫu 7)*

### PHIẾU ĐÁNH GIÁ KẾT QUẢ THỰC TẬP TỐT NGHIỆP

*(Do giảng viên hướng dẫn đánh giá — Mẫu 8)*

**Kết luận chương 3**

Chương 3 đã tổng hợp lại các kết quả cụ thể đạt được xuyên suốt đợt thực tập, được ghi nhận và xác nhận thông qua Mẫu 6, Mẫu 7 và Mẫu 8 đính kèm. Chương tiếp theo sẽ trình bày những kết luận và kiến nghị rút ra sau đợt thực tập.

# CHƯƠNG 4. KẾT LUẬN VÀ KIẾN NGHỊ

Qua đợt thực tập tại chương trình First Cloud AI Journey, em đã rút ra được nhiều bài học kinh nghiệm quý giá, cả về mặt kỹ thuật lẫn kỹ năng làm việc nhóm.

**Về mặt kỹ thuật:**

- Hiểu sâu hơn về kiến trúc Serverless trên AWS và cách áp dụng vào một dự án thực tế có người dùng.
- Nhận thức rõ tầm quan trọng của bảo mật và phân lập dữ liệu (multi-tenancy) trong các hệ thống SaaS đa người dùng — một lỗi tưởng chừng nhỏ có thể dẫn đến rò rỉ dữ liệu nghiêm trọng giữa các người dùng.
- Hiểu được giới hạn thực tế của các mô hình LLM/RAG và tầm quan trọng của việc kiểm chứng (grounding) câu trả lời để hạn chế hallucination.

**Về mặt kỹ năng mềm:**

- Tầm quan trọng của tinh thần đồng đội: bỏ qua "cái tôi" cá nhân để tập trung vào một giải pháp chung, chia rõ vai trò (backend/frontend/tài liệu) giúp nhóm làm việc hiệu quả hơn.
- Biết điểm dừng: giữa việc phát triển thêm tính năng mới và đảm bảo tiến độ, chất lượng của các tính năng cốt lõi.
- Ưu tiên đưa MVP (sản phẩm khả dụng tối thiểu) lên môi trường thật sớm để kiểm chứng, thay vì chỉ dừng lại ở lý thuyết.

**Kiến nghị:**

- Đối với doanh nghiệp (AWS/chương trình FCAJ): nên duy trì và mở rộng chương trình FCAJ cho nhiều khóa sinh viên hơn, vì mô hình "mentor đồng hành + dự án thực tế" mang lại giá trị thực hành rất lớn so với đào tạo lý thuyết thuần túy.
- Đối với cơ sở đào tạo (Trường Đại học Sài Gòn): nên tăng cường liên kết với các chương trình thực tập doanh nghiệp về Cloud/AI như FCAJ để sinh viên có cơ hội tiếp cận công nghệ mới sớm hơn.
- Đối với bản thân: cần trau dồi thêm kiến thức nền tảng về bảo mật hệ thống phân tán (distributed systems security) trước khi bắt đầu các dự án tương tự trong tương lai.

# TÀI LIỆU THAM KHẢO

1. Amazon Web Services, *AWS Documentation*, <https://docs.aws.amazon.com/>.
2. Amazon Web Services, *Amazon DynamoDB Developer Guide*, <https://docs.aws.amazon.com/dynamodb/>.
3. Amazon Web Services, *Amazon S3 User Guide — Using presigned URLs*, <https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html>.
4. Amazon Web Services, *Amazon Cognito Developer Guide*, <https://docs.aws.amazon.com/cognito/>.
5. Amazon Web Services, *Amazon Bedrock User Guide*, <https://docs.aws.amazon.com/bedrock/>.
6. Amazon Web Services, *AWS CodePipeline User Guide*, <https://docs.aws.amazon.com/codepipeline/>.
7. First Cloud AI Journey Study Group, *AWS Cloud Journey*, <https://cloudjourney.awsstudygroup.com/>.

# PHỤ LỤC

Các quy trình, tài liệu của doanh nghiệp mà sinh viên đã có trích dẫn trong quyển báo cáo thực tập tốt nghiệp (các tài liệu này cần được sự cho phép tiếp cận của doanh nghiệp thông qua chuyên gia doanh nghiệp hướng dẫn) *(văn bản gốc nếu có)*.

#### Quy định trình bày quyển báo cáo thực tập tốt nghiệp

- **Font:** Times New Roman
- Đóng bìa kiếng, in khổ giấy A4, in 1 mặt
- **Căn lề:** Lề trái: 3cm — Lề phải: 2cm — Lề trên: 2cm — Lề dưới: 2cm
- Đánh số trang vào cuối giữa trang, trang 1 bắt đầu từ Lời mở đầu. Các trang trước đó đánh i, ii, iii,... trừ trang bìa và trang lót bìa không đánh số trang.
- **Giãn dòng:** Từ 1.3 đến 1.5 lines
- Mục lục quyển báo cáo được đánh tự động
- Các hình vẽ, bảng biểu được đánh chỉ mục theo mỗi chương và phải có tiêu đề cho các bảng, hình vẽ; các công thức được đánh chỉ số (theo chương) ở bên phải
- Sinh viên chuyển cho 2 cán bộ hướng dẫn file PDF (1 file duy nhất chứa toàn bộ nội dung của quyển báo cáo thực tập tốt nghiệp)

| Cấp mục | Định dạng |
| --- | --- |
| Chương x | Size 16, in đậm, chữ hoa |
| x.1 | Size 14, in đậm, chữ hoa |
| x.1.1 | Size 13, in đậm |
| x.1.1.1 | Size 13, in nghiêng; đánh chỉ mục tối đa 4 cấp |
