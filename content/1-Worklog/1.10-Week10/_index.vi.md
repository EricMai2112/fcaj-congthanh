---
title: "Tuần 10: Hoàn thiện giao diện, kiểm thử toàn diện và video demo"
date: 2026-07-27
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Chủ đề:
Hoàn thiện trải nghiệm giao diện người dùng, kiểm thử toàn diện hệ thống, tự động hóa cảnh báo qua SES và ghi hình video demo kiến trúc dự án

### Mục tiêu tuần:
- Tinh chỉnh giao diện ứng dụng Chatpulse Frontend: tối ưu hóa hiển thị trên thiết bị di động và máy tính, thiết kế trải nghiệm nhắn tin mượt mà.
- Tiến hành kiểm thử toàn diện từ khâu đăng ký, xác thực OTP, nhắn tin thời gian thực, truyền nhận tệp đính kèm đến xử lý ngắt kết nối mạng.
- Cấu hình các CloudWatch Alarms giám sát chuyên sâu tự động kích hoạt gửi email cảnh báo thông qua Amazon SNS và SES.
- Đóng gói mã nguồn phiên bản hoàn chỉnh và quay video demo trực quan minh chứng toàn bộ kiến trúc và tính năng hoạt động thực tế trên AWS.

### Chi tiết công việc theo ngày (27/07/2026 - 31/07/2026):

| Ngày | Thứ | Nội dung công việc | Lab / Dự án thực hành | Nguồn tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| 27/07/2026 | Thứ 2 | - Hoàn thiện giao diện Chatpulse Frontend: tối ưu thanh Sidebar hiển thị danh sách phòng chat và trạng thái trực tuyến.<br>- Bổ sung modal xem trước hình ảnh phóng to và âm thanh thông báo tin nhắn mới.<br>- Đảm bảo giao diện hiển thị phù hợp trên cả trình duyệt máy tính và màn hình điện thoại. | Dự án Chatpulse: Tinh chỉnh giao diện và tối ưu hiển thị đa thiết bị | [React UI Best Practices](https://react.dev/learn) |
| 28/07/2026 | Thứ 3 | - Thiết lập kịch bản kiểm thử toàn diện:<br>+ Trường hợp 1: Đăng ký tài khoản mới, nhận OTP qua SES và kích hoạt tài khoản thành công.<br>+ Trường hợp 2: Đăng nhập cấp phát JWT, kết nối WebSocket qua Socket.io và gửi nhận tin nhắn văn bản tức thì.<br>+ Trường hợp 3: Tải ảnh avatar và tài liệu đính kèm định dạng PDF hoặc DOCX qua S3 Pre-signed URL.<br>+ Trường hợp 4: Xử lý tự động kết nối lại khi mạng bị ngắt. | Dự án Chatpulse: Kiểm thử tích hợp luồng nghiệp vụ toàn hệ thống | [End-to-End Testing Strategies](https://martinfowler.com/articles/practical-test-pyramid.html) |
| 29/07/2026 | Thứ 4 | - Thiết lập hệ thống giám sát cảnh báo trên Amazon CloudWatch:<br>+ Cảnh báo khi mức sử dụng CPU của EC2 vượt 75% liên tục trong 10 phút.<br>+ Cảnh báo khi mức sử dụng bộ nhớ của ElastiCache vượt 80%.<br>- Kết nối các Alarm tới Amazon SNS Topic, cấu hình tự động gửi email thông báo khẩn cấp cho đội ngũ vận hành. | Dự án Chatpulse: Thiết lập CloudWatch Alarms tự động kích hoạt cảnh báo qua SNS | [Amazon CloudWatch Alarm Actions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| 30/07/2026 | Thứ 5 | - Thực hiện đóng gói mã nguồn phiên bản ổn định v1.0.0, gắn Git Tag trên repository.<br>- Viết tài liệu hướng dẫn vận hành chi tiết: các biến môi trường cấu hình, quy trình phục hồi khi gặp sự cố.<br>- Chuẩn bị kịch bản thuyết trình và phân vai thuyết minh cho buổi báo cáo dự án. | Dự án Chatpulse: Đóng gói mã nguồn bản v1.0.0 và soạn thảo kịch bản Demo | [AWS Project Presentation Guide](https://aws.amazon.com/architecture/) |
| 31/07/2026 | Thứ 6 | - Tiến hành quay video demo dự án Chatpulse thời lượng khoảng 10 phút:<br>+ Phần 1: Giới thiệu tổng quan bài toán và sơ đồ kiến trúc chuẩn AWS Well-Architected.<br>+ Phần 2: Demo trực tiếp các tính năng chạy trên môi trường AWS thực tế: gửi nhận tin nhắn, upload media S3, kiểm tra log CloudWatch và phản ứng của AWS WAF.<br>+ Phần 3: Minh chứng hệ thống cảnh báo Alarms gửi email qua SNS.<br>- Biên tập video, xuất file chất lượng cao và lưu trữ an toàn. Tổng kết tuần 10. | Dự án Chatpulse: Ghi hình và biên tập Video Demo minh chứng dự án thực tế | [Screen Recording & Presentation Tools](https://obsproject.com/) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Kỹ năng kiểm thử tích hợp: phát hiện và xử lý các lỗi bất đồng bộ trong giao thức WebSocket.
  - Hiểu rõ cơ chế tự động hóa vận hành: hệ thống tự theo dõi sức khỏe và chủ động báo tin cho kỹ sư trước khi phát sinh sự cố gián đoạn dịch vụ.
  - Năng lực truyền đạt kỹ thuật và thuyết trình giải pháp qua sơ đồ kiến trúc đám mây và tính năng trực quan của sản phẩm.
- Kết quả đạt được:
  - Giao diện Chatpulse hoàn thiện, hiện đại, hoạt động mượt mà không có lỗi hiển thị.
  - Bộ kịch bản kiểm thử toàn diện vượt qua 100% các luồng nghiệp vụ cốt lõi.
  - 02 CloudWatch Alarms sẵn sàng bảo vệ hệ thống tính toán và lưu trữ đệm.
  - 01 Video demo ghi lại toàn bộ hoạt động thực tế của dự án.

### Khó khăn và hướng giải quyết:
- Khó khăn: Khi người dùng mất kết nối Internet tạm thời, kết nối WebSocket bị ngắt nhưng giao diện người dùng không tự động đồng bộ lại các tin nhắn bị bỏ lỡ trong thời gian mất mạng.
- Hướng giải quyết: Cải tiến phía Client: bắt sự kiện reconnect của Socket.io để tự động gửi yêu cầu gọi API kéo về các tin nhắn phát sinh trong thời gian ngoại tuyến, sau đó cập nhật lại vào trạng thái của ứng dụng. Nhờ vậy trải nghiệm nhắn tin luôn liền mạch và không bị mất dữ liệu.
