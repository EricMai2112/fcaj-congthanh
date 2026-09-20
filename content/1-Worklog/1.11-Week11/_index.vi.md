---
title: "Tuần 11: Tối ưu chi phí, đo lường hiệu năng và viết blog kỹ thuật"
date: 2026-08-03
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Chủ đề:
Rà soát tối ưu hóa chi phí đám mây, thiết lập S3 Lifecycle Rules, đo lường hiệu năng hệ thống và biên soạn bài viết kỹ thuật chia sẻ kiến trúc

### Mục tiêu tuần:
- Thực hiện phân tích và tối ưu hóa chi phí vận hành theo trụ cột của AWS Well-Architected Framework: tính toán chi phí bằng AWS Pricing Calculator và áp dụng quy tắc định cỡ tài nguyên hợp lý.
- Thiết lập chính sách vòng đời dữ liệu Amazon S3 Lifecycle Rules để tự động chuyển lớp lưu trữ và giảm thiểu chi phí lưu trữ lâu dài.
- Đo lường và đánh giá các chỉ số hiệu năng hệ thống dưới các kịch bản tải thực tế.
- Biên soạn bài viết kỹ thuật chuyên sâu phân tích chi tiết giải pháp kiến trúc dự án Chatpulse để chia sẻ lên cộng đồng AWS Study Group.

### Chi tiết công việc theo ngày (03/08/2026 - 07/08/2026):

| Ngày | Thứ | Nội dung công việc | Lab / Dự án thực hành |
| :--- | :--- | :--- | :--- |
| 03/08/2026 | Thứ 2 | - Sử dụng công cụ AWS Pricing Calculator để lập bảng dự toán chi phí chi tiết cho hệ thống Chatpulse ở quy mô 1.000 người dùng hoạt động hàng ngày.<br>- Phân tích cấu trúc chi phí: máy chủ tính toán EC2, ElastiCache Redis, dung lượng S3, lưu lượng truyền mạng CloudFront và chi phí xử lý qua NAT Gateway.<br>- Xác định các điểm lãng phí tài nguyên và đề xuất phương án tối ưu hóa chi phí định kỳ. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 04/08/2026 | Thứ 3 | - Thiết lập quy tắc vòng đời dữ liệu S3 Lifecycle Configuration trên bucket chatpulse-bucket:<br>+ Chuyển tệp tin sau 30 ngày từ S3 Standard sang S3 Standard-IA giúp tiết kiệm chi phí lưu trữ.<br>+ Chuyển tiếp sau 90 ngày sang S3 Glacier Flexible Retrieval cho mục đích sao lưu lưu trữ lâu dài.<br>+ Tự động xóa các bản tải lên dở dang không hoàn tất sau 7 ngày. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 05/08/2026 | Thứ 4 | - Thực hiện rà soát và định cỡ tài nguyên hạ tầng tính toán: Đánh giá mức sử dụng CPU và bộ nhớ thực tế của EC2 và ElastiCache node.<br>- Chuyển đổi instance sang dòng tiết kiệm năng lượng AWS Graviton t4g hoặc giữ cấu hình t3.micro để tận dụng tối đa gói Free Tier.<br>- Lên kế hoạch tắt các máy chủ lab phụ trợ ngoài giờ làm việc bằng AWS Instance Scheduler để tiết kiệm chi phí môi trường phát triển. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 06/08/2026 | Thứ 5 | - Tiến hành đo lường các chỉ số hiệu năng cốt lõi của hệ thống Chatpulse:<br>+ Độ trễ truyền nhận tin nhắn WebSocket hai chiều: Đạt trung bình 24ms.<br>+ Thời gian tải trang ban đầu qua CloudFront: Giảm từ 380ms xuống còn 65ms nhờ bộ nhớ đệm tại Edge Locations.<br>+ Tốc độ tải tệp tin lên S3 qua Pre-signed URL đạt băng thông tối đa của mạng client mà không gây áp lực lên máy chủ backend. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 07/08/2026 | Thứ 6 | - Biên soạn bài viết kỹ thuật chuyên sâu: Xây dựng nền tảng truyền thông doanh nghiệp thời gian thực độ trễ thấp, bảo mật và tối ưu chi phí trên AWS.<br>- Trình bày rõ ràng bài toán, sơ đồ kiến trúc, giải pháp giải quyết nghẽn cổ chai với Redis Pub/Sub, luồng tải S3 Pre-signed URL và cơ chế bảo vệ của AWS WAF.<br>- Gửi bản thảo cho Mentor duyệt và đăng bài lên nhóm cộng đồng AWS Study Group. Tổng kết tuần 11. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Thấu hiểu nguyên lý tối ưu hóa chi phí trong kiến trúc đám mây: kiến trúc tốt phải vận hành hiệu quả với mức chi phí hợp lý nhất cho doanh nghiệp.
  - Nắm vững các lớp lưu trữ của Amazon S3 và cách khai thác vòng đời tự động để tiết kiệm chi phí lưu trữ lâu dài.
  - Kỹ năng phân tích hiệu năng hệ thống thực tế thông qua các chỉ số định lượng cụ thể.
  - Kỹ năng đúc kết tri thức và đóng góp giá trị chuyên môn cho cộng đồng công nghệ điện toán đám mây.
- Kết quả đạt được:
  - Bảng dự toán chi phí chi tiết cho hệ thống Chatpulse với chi phí vận hành ước tính chỉ khoảng 15 đến 25 USD một tháng cho quy mô doanh nghiệp vừa và nhỏ.
  - Quy tắc S3 Lifecycle Rules được kích hoạt thành công trên bucket dữ liệu.
  - Báo cáo đo lường hiệu năng hệ thống với các chỉ số đo lường thực tế.
  - 01 Bài viết Technical Blog chuyên sâu được xuất bản trên cộng đồng AWS Study Group.

### Khó khăn và hướng giải quyết:
- Khó khăn: Chi phí phát sinh từ NAT Gateway trong quá trình kiểm thử truyền tải file lớn do NAT Gateway tính phí trên mỗi GB dữ liệu đi qua.
- Hướng giải quyết: Phân tích luồng mạng và nhận thấy việc chuyển hướng tải file từ client trực tiếp lên S3 đã tránh được việc file đi qua NAT Gateway. Đồng thời, đối với kết nối nội bộ từ EC2 đến S3, tạo thêm Amazon S3 Gateway VPC Endpoint hoàn toàn miễn phí. Nhờ vậy, mọi lưu lượng truy cập từ các dịch vụ trong VPC đến S3 đều đi qua đường nội bộ của AWS mà không cần đi qua NAT Gateway, giúp tiết kiệm chi phí mạng.
