---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---
### Mục tiêu tuần 6:

* Review và chỉnh sửa lại nội dung Workshop (mục 5) cho rõ ràng, nhất quán hơn.
* Đăng 3 bài blog kỹ thuật đã chuẩn bị lên cộng đồng AWS Study Group.
* Hoàn thiện 4 diagram kiến trúc chính (Storage Structure, Lambda Modules, CI/CD Pipeline, Cleanup Flow) và cross-check lại với các thành viên trong nhóm.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Lên văn phòng. Review và chỉnh sửa lại nội dung mục Workshop cho rõ ràng, nhất quán hơn <br>&emsp;+ Đọc lại toàn bộ mục 5-Workshop, thống nhất lại văn phong và thuật ngữ giữa các phần do nhiều thành viên viết <br>&emsp;+ Sửa các đoạn diễn đạt chưa rõ ràng, bổ sung ví dụ cụ thể ở những chỗ còn chung chung | 27/07/2026 | 27/07/2026 | |
| 3 | - Đăng Blog 1 (EventBridge Scheduler), Blog 2 (Cold start), Blog 3 (Lambda Tenant Isolation) lên nhóm Facebook AWS Study Group <br>&emsp;+ Biên tập lại nội dung từ báo cáo Workshop đầy đủ thành phiên bản phù hợp để đăng lên Facebook (lược bỏ bảng và hình ảnh, bổ sung phần giải thích lý do lựa chọn giải pháp kỹ thuật để làm rõ luận điểm) <br>&emsp;+ Đăng lần lượt từng bài, theo dõi phản hồi/bình luận trong nhóm | 28/07/2026 | 28/07/2026 | <https://www.facebook.com/groups/awsstudygroupfcj> |
| 4 | - Lên văn phòng. Chỉnh sửa lại 4 diagram kiến trúc (Storage Structure, Lambda Modules, CI/CD Pipeline, Cleanup Flow) trên draw.io <br>&emsp;+ Cập nhật diagram CI/CD Pipeline để thể hiện đúng bước CodeBuild cho cả Frontend lẫn Backend (trước đó vẽ thiếu bước CodeBuild của Frontend) <br> - Xuất lại hình ảnh diagram mới vào mục 5.1.3 <br>&emsp;+ Export PNG độ phân giải cao, thay thế ảnh cũ, kiểm tra lại đường dẫn ảnh trong Markdown không bị vỡ <br> - Cross-check lại các diagram với các thành viên khác trong nhóm <br>&emsp;+ Gửi bản xem trước cho Trọng và Phong xác nhận diagram khớp với những gì mỗi người đã triển khai thật <br> - Bổ sung các ảnh chụp test còn thiếu vào mục System Testing (5.5) <br>&emsp;+ Chụp lại màn hình các test case còn thiếu ảnh minh họa (đăng nhập, upload tài liệu, chat RAG) | 29/07/2026 | 29/07/2026 | <https://l2nt.github.io/AWS-Report-LeNguyenNhatTam/5-workshop/5.1-workshop-overview/5.1.3--overall-aws-architecture/> |
| 5 | - Chỉnh sửa lại nội dung Mẫu 9 (Nhật ký thực tập) <br>&emsp;+ Bổ sung nội dung thực tế của nhóm thay cho phần hướng dẫn chung, sửa lại đúng sĩ số nhóm (5 sinh viên: Tâm, Phong, Trọng, Nam, Phúc) <br>&emsp;+ Tách rõ nội dung báo cáo Workshop (mục 1-7, nộp cho chương trình FCJ) với các mẫu nộp trường (mục 16-19), tránh nhầm lẫn giữa hai tài liệu | 30/07/2026 | 30/07/2026 | |
| 6 | - Điền các thông tin cá nhân/nhóm còn thiếu trong các mẫu nộp trường <br>&emsp;+ Mẫu 6: bổ sung thông tin liên hệ GVHD (email, số điện thoại) <br>&emsp;+ Mẫu 7: bổ sung địa chỉ doanh nghiệp thực tập <br>&emsp;+ Mẫu 8: rà soát và sửa lại đánh số đề mục "III. Điểm tổng kết" cho đúng thứ tự <br> - Build lại site (hugo --minify) để kiểm tra không phát sinh lỗi sau khi chỉnh sửa | 31/07/2026 | 31/07/2026 | |
| 7 | - Cập nhật lại Blog 2 theo phản hồi từ admin nhóm Facebook AWS Study Group (bài viết cũ bị từ chối duyệt) <br>&emsp;+ Thay bằng bài viết đã được duyệt của một thành viên trong nhóm (Phong), có ghi chú rõ nguồn và số lượng blog vẫn tính đủ theo quy định (3 bài/nhóm) <br> - Khắc phục lỗi liên kết logo trên trang báo cáo bị dẫn sai sang trang cá nhân khác, sửa lại trỏ đúng về trang báo cáo <br> - Rà soát lại toàn bộ báo cáo lần cuối trước khi bước sang tuần nộp Workshop | 01/08/2026 | 01/08/2026 | |


### Kết quả đạt được tuần 6:

* Review và chỉnh sửa lại nội dung mục Workshop (5-Workshop) cho rõ ràng, nhất quán hơn.
* Đăng Blog 1/2/3 lên nhóm Facebook AWS Study Group - xem chi tiết tại mục 3.1-3.3.
* Chỉnh sửa và hoàn thiện 4 diagram kiến trúc (Storage Structure, Lambda Modules, CI/CD Pipeline, Cleanup Flow) trên draw.io, đã cross-check với các thành viên trong nhóm để đảm bảo chính xác.
* Xuất lại hình ảnh diagram mới vào mục 5.1.3 (Overall AWS Architecture).
* Bổ sung các ảnh chụp test còn thiếu vào mục System Testing (5.5).
* Hoàn thiện nội dung Mẫu 9 với thông tin thực tế của nhóm, điền đầy đủ thông tin còn thiếu trong Mẫu 6, Mẫu 7, Mẫu 8.
* Cập nhật lại Blog 2 theo yêu cầu của admin nhóm Facebook, khắc phục lỗi liên kết logo trên trang báo cáo.
* ...


