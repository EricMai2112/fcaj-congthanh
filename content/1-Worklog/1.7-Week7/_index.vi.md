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
- Khởi tạo máy chủ ứng dụng Amazon EC2 trong Public Subnet và cụm Amazon ElastiCache Redis trong Private Subnet làm bộ nhớ đệm và điều phối tin nhắn Pub/Sub.

### Chi tiết công việc theo ngày (06/07/2026 - 10/07/2026):

| Ngày | Thứ | Nội dung công việc | Lab / Dự án thực hành |
| :--- | :--- | :--- | :--- |
| 06/07/2026 | Thứ 2 | - Khởi tạo GitHub Repository cho dự án Chatpulse, thiết lập các quy tắc bảo vệ nhánh chính.<br>- Khởi tạo cấu trúc source code: Frontend sử dụng React, Tailwind CSS và Vite, Backend sử dụng Node.js, Express và TypeScript.<br>- Thiết lập quy chuẩn kiểm tra code với ESLint, Prettier và file cấu hình môi trường mẫu .env.example. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 07/07/2026 | Thứ 3 | - Xây dựng module xác thực trên Backend: thiết kế mô hình dữ liệu người dùng Users, mã hóa mật khẩu an toàn bằng bcrypt.<br>- Lập trình các API đăng ký, đăng nhập và làm mới token.<br>- Triển khai cơ chế token kép: Access Token thời hạn 15 phút và Refresh Token thời hạn 7 ngày lưu trong HTTP-only cookie. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 08/07/2026 | Thứ 4 | - Cấu hình dịch vụ gửi email Amazon SES tại region Singapore ap-southeast-1.<br>- Thực hiện xác thực địa chỉ email gửi đi trong môi trường SES Sandbox.<br>- Tích hợp AWS SDK for JavaScript vào backend: viết service tạo mã OTP 6 chữ số ngẫu nhiên, lưu vào bộ đệm và gửi email kích hoạt tài khoản người dùng mới. | [000077 - Tích hợp hệ thống gửi thông báo với AWS](https://000077.awsstudygroup.com/vi/) |
| 09/07/2026 | Thứ 5 | - Khởi tạo ElastiCache Subnet Group trải dài trên 2 Private Data Subnets.<br>- Khởi tạo cluster Amazon ElastiCache Redis phiên bản 7.x, node type cache.t3.micro.<br>- Cấu hình Security Group cho Redis: chỉ cho phép cổng 6379 từ Security Group của EC2 App Server.<br>- Cấu hình thời gian sống TTL cho việc lưu trữ tạm mã OTP và phiên làm việc. | [000061 - Bộ nhớ đệm trong bộ nhớ với Amazon ElastiCache](https://000061.awsstudygroup.com/vi/) |
| 10/07/2026 | Thứ 6 | - Khởi tạo máy chủ EC2 Backend Ubuntu 22.04 LTS trong Public Subnet.<br>- Cài đặt Node.js, PM2 process manager và clone mã nguồn backend.<br>- Kiểm tra kết nối mạng nội bộ từ EC2 đến ElastiCache Redis Endpoint trong Private Subnet bằng lệnh redis-cli ping.<br>- Tổng kết tuần 7 và chạy thử nghiệm luồng đăng ký tài khoản nhận OTP. | [000004 - Triển khai Backend Node.js trên EC2](https://000004.awsstudygroup.com/vi/) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Mô hình xác thực kết hợp Access Token và Refresh Token giúp hệ thống mở rộng linh hoạt mà không cần duy trì phiên làm việc nặng trên database.
  - Quy trình vận hành và nguyên tắc gửi thư an toàn qua Amazon SES trong môi trường Sandbox.
  - Vai trò của Amazon ElastiCache Redis: đóng vai trò như một kho dữ liệu In-memory tốc độ cao để lưu trữ tạm thời OTP, trạng thái trực tuyến và làm nền tảng Pub/Sub cho WebSocket.
- Kết quả đạt được:
  - Mã nguồn Backend Node.js và Express hoàn chỉnh cho toàn bộ luồng xác thực và gửi OTP qua SES.
  - Cụm Amazon ElastiCache Redis hoạt động ổn định trong Private Subnet, được bảo vệ chặt chẽ.
  - Máy chủ EC2 Backend trong Public Subnet kết nối thông suốt với Redis trong Private Subnet.

### Khó khăn và hướng giải quyết:
- Khó khăn: Ban đầu máy chủ EC2 trong Public Subnet chưa kết nối được tới ElastiCache Redis đặt trong Private Subnet.
- Hướng giải quyết: Cấu hình Inbound rule của Security Group cho ElastiCache Redis chỉ cho phép cổng 6379 từ Security Group của máy chủ EC2 Backend, bảo đảm kết nối thông suốt và an toàn tuyệt đối.
