---
title: "Tuần 7: Khởi tạo mã nguồn, Backend Auth, SES và ElastiCache Redis"
date: 2026-07-06
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Chủ đề:
Khởi tạo cấu trúc mã nguồn dự án, phát triển hệ thống xác thực backend với Node.js, Express, tích hợp Amazon SES và triển khai cụm Amazon ElastiCache Redis

### Mục tiêu tuần:
- Thiết lập hệ thống quản lý mã nguồn Git, chuẩn hóa quy trình phân nhánh cho dự án Chatpulse gồm Frontend React và Backend Node.js.
- Phát triển hệ thống xác thực người dùng an toàn: cơ chế xác thực với JSON Web Token, mã hóa mật khẩu với bcrypt.
- Cấu hình dịch vụ Amazon SES xác thực danh tính gửi thư và lập trình luồng gửi mã OTP kích hoạt tài khoản hoặc khôi phục mật khẩu.
- Khởi tạo máy chủ ứng dụng Amazon EC2 trong Private Subnet và cụm Amazon ElastiCache Redis làm bộ nhớ đệm và điều phối tin nhắn Pub/Sub.

### Chi tiết công việc theo ngày (06/07/2026 - 10/07/2026):

| Ngày | Thứ | Nội dung công việc | Lab / Dự án thực hành | Nguồn tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| 06/07/2026 | Thứ 2 | - Khởi tạo GitHub Repository cho dự án Chatpulse; thiết lập các quy tắc bảo vệ nhánh chính.<br>- Khởi tạo cấu trúc source code: Frontend sử dụng React, Tailwind CSS và Vite; Backend sử dụng Node.js, Express và TypeScript.<br>- Thiết lập quy chuẩn kiểm tra code với ESLint, Prettier và file cấu hình môi trường mẫu .env.example. | Dự án Chatpulse: Thiết lập Repository, cấu trúc thư mục và khởi tạo ban đầu | [Gitflow Workflow Guide](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) |
| 07/07/2026 | Thứ 3 | - Xây dựng module xác thực trên Backend: thiết kế mô hình dữ liệu người dùng Users, mã hóa mật khẩu an toàn bằng bcrypt.<br>- Lập trình các API đăng ký, đăng nhập và làm mới token.<br>- Triển khai cơ chế token kép: Access Token thời hạn 15 phút và Refresh Token thời hạn 7 ngày lưu trong HTTP-only cookie. | Dự án Chatpulse: Xây dựng module xác thực JWT an toàn cho API | [JWT Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_for_Java_Cheat_Sheet.html) |
| 08/07/2026 | Thứ 4 | - Cấu hình dịch vụ gửi email Amazon SES tại region Singapore ap-southeast-1.<br>- Thực hiện xác thực địa chỉ email gửi đi trong môi trường SES Sandbox.<br>- Tích hợp AWS SDK for JavaScript vào backend: viết service tạo mã OTP 6 chữ số ngẫu nhiên, lưu vào bộ đệm và gửi email kích hoạt tài khoản người dùng mới. | Dự án Chatpulse: Tích hợp Amazon SES gửi email mã OTP kích hoạt | [Amazon SES Developer Guide](https://docs.aws.amazon.com/ses/latest/dg/) |
| 09/07/2026 | Thứ 5 | - Khởi tạo ElastiCache Subnet Group trải dài trên 2 Private Data Subnets.<br>- Khởi tạo cluster Amazon ElastiCache Redis phiên bản 7.x, node type cache.t3.micro.<br>- Cấu hình Security Group cho Redis: chỉ cho phép cổng 6379 từ Security Group của EC2 App Server.<br>- Cấu hình thời gian sống TTL cho việc lưu trữ tạm mã OTP và phiên làm việc. | Dự án Chatpulse: Triển khai cụm Amazon ElastiCache Redis trong Private Subnet | [Amazon ElastiCache Guide](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/) |
| 10/07/2026 | Thứ 6 | - Khởi tạo máy chủ EC2 Backend Ubuntu 22.04 LTS trong Private App Subnet.<br>- Cài đặt Node.js, PM2 process manager và clone mã nguồn backend.<br>- Kiểm tra kết nối mạng nội bộ từ EC2 đến ElastiCache Redis Endpoint bằng lệnh redis-cli ping.<br>- Tổng kết tuần 7 và chạy thử nghiệm luồng đăng ký tài khoản nhận OTP. | Dự án Chatpulse: Triển khai Backend lên EC2 Private Subnet và kiểm thử Redis | [PM2 Production Process Manager](https://pm2.keymetrics.io/docs/usage/quick-start/) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Mô hình xác thực kết hợp Access Token và Refresh Token giúp hệ thống mở rộng linh hoạt mà không cần duy trì phiên làm việc nặng trên database.
  - Quy trình vận hành và nguyên tắc gửi thư an toàn qua Amazon SES trong môi trường Sandbox.
  - Vai trò của Amazon ElastiCache Redis: đóng vai trò như một kho dữ liệu In-memory tốc độ cao để lưu trữ tạm thời OTP, trạng thái trực tuyến và làm nền tảng Pub/Sub cho WebSocket.
- Kết quả đạt được:
  - Mã nguồn Backend Node.js và Express hoàn chỉnh cho toàn bộ luồng xác thực và gửi OTP qua SES.
  - Cụm Amazon ElastiCache Redis hoạt động ổn định trong Private Subnet, được bảo vệ chặt chẽ.
  - Máy chủ EC2 Backend trong Private Subnet kết nối thông suốt với Redis.

### Khó khăn và hướng giải quyết:
- Khó khăn: Máy chủ EC2 đặt trong Private Subnet không có Public IP nên không thể tải các package Node.js qua lệnh npm install và không kết nối được đến GitHub để kéo mã nguồn.
- Hướng giải quyết: Kiểm tra lại bảng định tuyến của Private App Subnet, phát hiện route table chưa định tuyến 0.0.0.0/0 qua NAT Gateway trong Public Subnet. Sau khi cấu hình định tuyến ra NAT Gateway, máy chủ trong Private Subnet đã truy cập Internet tải package bình thường trong khi vẫn bảo đảm không nhận kết nối lạ từ bên ngoài.
