---
title: "Tuần 8: Chat thời gian thực, tải file lên S3 và tên miền SSL"
date: 2026-07-13
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Chủ đề:
Xây dựng hệ thống chat thời gian thực với WebSocket và Redis Pub/Sub, luồng tải file trực tiếp lên Amazon S3 bằng Pre-signed URL và cấu hình tên miền SSL với ACM và CloudFront

### Mục tiêu tuần:
- Phát triển tính năng nhắn tin thời gian thực sử dụng WebSocket và Socket.io tích hợp cơ chế Redis Adapter để đồng bộ tin nhắn đa máy chủ.
- Lập trình quy trình tải tài liệu, hình ảnh, avatar trực tiếp từ giao diện Client lên Amazon S3 bằng cơ chế Pre-signed URL có chữ ký bảo mật ngắn hạn.
- Quản lý tên miền dự án Chatpulse thông qua Amazon Route 53, yêu cầu và xác thực chứng chỉ số SSL/TLS từ AWS Certificate Manager.
- Khởi tạo Amazon CloudFront Distribution phân phối nội dung tĩnh Frontend React, kích hoạt giao thức bảo mật HTTPS bắt buộc trên toàn hệ thống.

### Chi tiết công việc theo ngày (13/07/2026 - 17/07/2026):

| Ngày | Thứ | Nội dung công việc | Lab / Dự án thực hành | Nguồn tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| 13/07/2026 | Thứ 2 | - Tích hợp Socket.io vào máy chủ Backend Node.js; viết middleware xác thực JWT cho handshake connection của WebSocket.<br>- Tích hợp socket.io redis-adapter kết nối trực tiếp với cụm ElastiCache Redis.<br>- Kiểm thử gửi nhận tin nhắn văn bản giữa 2 tab trình duyệt với độ trễ phản hồi tức thì. | Dự án Chatpulse: Xây dựng WebSocket Server với Redis Pub/Sub Adapter | [Socket.io Redis Adapter](https://socket.io/docs/v4/redis-adapter/) |
| 14/07/2026 | Thứ 3 | - Phát triển các tính năng nhắn tin: chat cá nhân và chat theo phòng ban nội bộ.<br>- Lập trình sự kiện phát hiện trạng thái trực tuyến của người dùng lưu trữ trên Redis.<br>- Bổ sung tính năng hiển thị trạng thái đang nhập tin nhắn và cơ chế đánh dấu tin nhắn đã nhận. | Dự án Chatpulse: Hoàn thiện các sự kiện Chat phòng ban và User Presence | [WebSocket Security Best Practices](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html#websockets) |
| 15/07/2026 | Thứ 4 | - Lập trình API media upload-url trên Backend: sử dụng AWS SDK for S3 để sinh S3 Pre-signed PUT URL có thời hạn hợp lệ trong 300 giây.<br>- Xây dựng component upload trên React Client: gửi yêu cầu lấy link ký điện tử, gửi trực tiếp file lên S3 Bucket và lưu URL tài nguyên vào cơ sở dữ liệu.<br>- Kiểm tra luồng upload ảnh đại diện và tài liệu đính kèm định dạng PDF, DOCX, PNG, JPG. | Dự án Chatpulse: Lập trình luồng Upload Media an toàn bằng S3 Pre-signed URL | [S3 Pre-signed URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html) |
| 16/07/2026 | Thứ 5 | - Cấu hình tên miền phụ dự án trên Amazon Route 53.<br>- Yêu cầu cấp phát chứng chỉ số công khai SSL/TLS thông qua AWS Certificate Manager tại region us-east-1.<br>- Tạo tự động các bản ghi CNAME trên Route 53 để hoàn tất quy trình xác thực DNS. | Dự án Chatpulse: Quản lý DNS Route 53 và cấp chứng chỉ SSL/TLS qua ACM | [AWS Certificate Manager Guide](https://docs.aws.amazon.com/acm/latest/userguide/) |
| 17/07/2026 | Thứ 6 | - Đóng gói mã nguồn React Frontend thành bộ file tĩnh HTML, JS, CSS tối ưu.<br>- Đồng bộ file tĩnh lên S3 Bucket Hosting và khởi tạo Amazon CloudFront Distribution có gắn SSL Certificate từ ACM.<br>- Cấu hình chính sách chuyển hướng HTTP sang HTTPS và thiết lập Route 53 Alias Record trỏ tên miền chính về CloudFront. Tổng kết tuần 8. | Dự án Chatpulse: Triển khai CloudFront CDN HTTPS và cấu hình Route 53 Alias | [CloudFront HTTPS Configuration](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-alternate-domain-names.html) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Giải quyết bài toán mở rộng ngang của kết nối WebSocket: việc sử dụng Redis Pub/Sub Adapter giúp các client kết nối ở các máy chủ khác nhau vẫn nhận được tin nhắn của nhau đồng thời.
  - Hiểu sâu cơ chế Pre-signed URL: trao quyền ghi có kiểm soát và giới hạn thời gian cho client mà không công khai Access Key hay mở quyền ghi công khai cho S3 Bucket.
  - Nắm vững quy trình cấu hình chứng chỉ mã hóa SSL/TLS với ACM và cơ chế định tuyến tên miền toàn cầu với Route 53 và CloudFront.
- Kết quả đạt được:
  - Module Chat thời gian thực hoạt động mượt mà, phản hồi tin nhắn văn bản dưới 30ms.
  - Luồng tải tệp tin và ảnh đại diện hoạt động ổn định, lưu trữ an toàn trên S3.
  - Website Frontend dự án Chatpulse được phân phối qua CloudFront với giao thức bảo mật HTTPS.

### Khó khăn và hướng giải quyết:
- Khó khăn: Trình duyệt báo lỗi mạng và quyền truy cập khi frontend gọi phương thức HTTP PUT để đẩy file lên Amazon S3 thông qua Pre-signed URL vừa nhận được từ backend.
- Hướng giải quyết: Kiểm tra cấu hình S3 Bucket CORS. Phát hiện S3 Bucket chỉ mới cho phép GET và chưa khai báo header Content-Type. Cấu hình lại file CORS trên S3 Bucket bổ sung phương thức PUT và cho phép header từ CloudFront domain của dự án, giúp client tải file thành công.
