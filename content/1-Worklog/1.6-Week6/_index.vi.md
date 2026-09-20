---
title: "Tuần 6: Khởi động dự án Chatpulse, thiết kế kiến trúc và mạng VPC"
date: 2026-06-29
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Chủ đề:
Khởi động dự án thực tập Chatpulse, phân tích yêu cầu kỹ thuật, thiết kế kiến trúc AWS Well-Architected và triển khai mạng VPC chuyên dụng

### Mục tiêu tuần:
- Chính thức khởi động dự án thực tập cá nhân Chatpulse, một nền tảng giao tiếp và truyền thông nội bộ doanh nghiệp thời gian thực.
- Phân tích yêu cầu chức năng bao gồm quản lý người dùng, chat tức thì, chia sẻ file, phân quyền và yêu cầu phi chức năng về bảo mật, độ trễ thấp và tối ưu chi phí.
- Vẽ sơ đồ kiến trúc tổng thể của hệ thống Chatpulse trên AWS sử dụng bộ ký hiệu AWS Architecture Icons chuẩn mực, đáp ứng 5 trụ cột của AWS Well-Architected Framework.
- Thiết kế và khởi tạo hạ tầng mạng Amazon VPC chuyên dụng cùng cấu hình Amazon S3 Bucket lưu trữ dữ liệu truyền thông đa phương tiện.

### Chi tiết công việc theo ngày (29/06/2026 - 03/07/2026):

| Ngày       | Thứ   | Nội dung công việc                                                                                                                                                                                                                                                                                                                           | Lab / Dự án thực hành                                                                                                                 |
| :--------- | :---- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| 29/06/2026 | Thứ 2 | - Phân tích các luồng nghiệp vụ chính: Đăng ký, đăng nhập an toàn, nhắn tin thời gian thực qua WebSocket, tải tệp tài liệu và hình ảnh trực tiếp lên Cloud.<br>- Lập kế hoạch phân chia giai đoạn phát triển và mốc bàn giao trong các tuần tiếp theo.                                                                                     | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse)                                                                            |
| 30/06/2026 | Thứ 3 | - Phác thảo sơ đồ kiến trúc tổng thể bằng công cụ Draw.io sử dụng bộ chuẩn AWS Architecture Icons.<br>- Thiết kế luồng dữ liệu 3 tầng: Client đến CloudFront, đến ALB, đến EC2 App Instances chạy Node.js và Socket.io trong Public Subnet, kết nối tới ElastiCache Redis trong Private Subnet, S3 và SES.<br>- Tự tay chỉnh sửa từng chi tiết, bảo đảm luồng dữ liệu hợp lý và đúng tên dịch vụ AWS. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse)                                                                            |
| 01/07/2026 | Thứ 4 | - Đánh giá sơ đồ kiến trúc theo 5 trụ cột AWS Well-Architected:<br>+ Về bảo mật: Triển khai EC2 backend trong Public Subnet, cô lập ElastiCache trong Private Subnet, truy cập S3 qua Pre-signed URL.<br>+ Về độ tin cậy và hiệu năng: Phân tán trên 2 vùng khả dụng, tận dụng Redis Pub/Sub đồng bộ tin nhắn đa máy chủ.<br>+ Về tối ưu chi phí: Tận dụng các dòng máy chủ tiết kiệm và cấu hình lưu trữ hợp lý. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse)                                                                            |
| 02/07/2026 | Thứ 5 | - Triển khai mạng VPC chuyên biệt cho dự án Chatpulse dải 10.10.0.0/16.<br>- Thiết lập cấu trúc mạng: 02 Public Subnets cho ALB và EC2 Backend, 02 Private Data Subnets cho ElastiCache Redis.<br>- Gắn kết Internet Gateway và cấu hình các bảng định tuyến Route Tables tương ứng.                                                      | [000003 - Triển khai hạ tầng Multi-tier VPC](https://000003.awsstudygroup.com/vi/)                                                    |
| 03/07/2026 | Thứ 6 | - Khởi tạo Amazon S3 Bucket chuyên dụng lưu trữ media cho Chatpulse mang tên chatpulse-bucket.<br>- Cấu hình Block Public Access toàn bộ.<br>- Cấu hình CORS policy cho phép client gửi các yêu cầu HTTP PUT và GET upload tệp trực tiếp.<br>- Tổng kết tuần 6 và báo cáo sơ đồ kiến trúc cho Mentor duyệt.                             | [000057 - Khởi tạo và bảo mật S3 Bucket lưu trữ Media](https://000057.awsstudygroup.com/vi/)                                         |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Khả năng chuyển hóa bài toán nghiệp vụ doanh nghiệp thành giải pháp kiến trúc điện toán đám mây theo chuẩn mực của AWS.
  - Áp dụng các tiêu chí bảo mật theo chiều sâu, phân tách ranh giới mạng giữa tầng Web, tầng Ứng dụng và tầng Dữ liệu.
  - Hiểu rõ cơ chế kết hợp giữa cơ sở dữ liệu và bộ nhớ đệm In-memory Redis để đáp ứng nhiều kết nối WebSocket đồng thời.
- Kết quả đạt được:
  - Bản vẽ sơ đồ kiến trúc tổng thể dự án Chatpulse đạt chuẩn AWS Architecture, sẵn sàng đưa vào Proposal và Workshop.
  - Hạ tầng mạng chatpulse-vpc gồm Public Subnets cho EC2 Backend và Private Subnets cho ElastiCache Redis đã được triển khai và kiểm tra định tuyến thành công.
  - S3 Bucket chatpulse-bucket đã được khởi tạo và sẵn sàng tiếp nhận luồng tải tệp.

### Khó khăn và hướng giải quyết:
- Khó khăn: Ban đầu sơ đồ kiến trúc dự định cho phép client upload file media thông qua máy chủ EC2 backend, tuy nhiên máy chủ EC2 sẽ bị nghẽn băng thông và tốn tài nguyên xử lý dữ liệu khi nhiều người dùng tải file dung lượng lớn cùng lúc.
- Hướng giải quyết: Áp dụng giải pháp chuẩn của AWS: chuyển đổi mô hình sang cơ chế S3 Pre-signed URL. Máy chủ EC2 chỉ làm nhiệm vụ xác thực quyền hạn và tạo URL có chữ ký bảo mật trong thời gian ngắn, sau đó client tải file trực tiếp lên Amazon S3. Thiết kế này giải phóng hoàn toàn tải mạng cho máy chủ backend.
