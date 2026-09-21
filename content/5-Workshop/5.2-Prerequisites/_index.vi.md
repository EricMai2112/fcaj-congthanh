---
title: "Các bước chuẩn bị"
date: 2026-06-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---


Trước khi bắt đầu các bước triển khai kỹ thuật cho dự án ChatPulse, người thực hiện cần hoàn thành các bước chuẩn bị nền tảng về tài khoản đám mây, môi trường phát triển máy cá nhân, mã nguồn và các dịch vụ dữ liệu bên ngoài.

---

### 1. Tài Khoản AWS & Khởi Tạo IAM User

- **Tài khoản AWS:** Chuẩn bị 01 tài khoản AWS đang hoạt động, tốt nhất nằm trong diện ưu đãi AWS Free Tier để tối ưu chi phí thực hành.
- **Khởi tạo IAM User chuyên dụng:** Thay vì sử dụng tài khoản Root cho các hoạt động thường ngày, khởi tạo một người dùng IAM quản trị riêng biệt mang tên `eric-thanh` với các quyền hạn phù hợp.
- **Tạo Access Key quản trị:** Tạo cặp khóa truy cập Access Key ID và Secret Access Key đang ở trạng thái kích hoạt (Active) để phục vụ việc kết nối từ xa và cấu hình công cụ quản trị.
- **Cấu hình công cụ AWS CLI:** Cài đặt công cụ AWS CLI trên máy tính cá nhân, đăng nhập thông qua Access Key của người dùng IAM và cấu hình vùng mặc định ap-southeast-1.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.2-Prerequisite/iam-user-setup.jpg" alt="Minh chứng cấu hình IAM User eric-thanh" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.2: Minh chứng thông tin khởi tạo và cấu hình thông tin xác thực của IAM User eric-thanh</p>
</div>

---

### 2. Môi Trường Làm Việc Trên Máy Cá Nhân

- **Cài đặt Node.js:** Cài đặt môi trường runtime Node.js phiên bản ổn định LTS phục vụ việc chạy thử nghiệm và kiểm tra các gói thư viện phụ thuộc.
- **Công cụ quản lý mã nguồn:** Cài đặt công cụ Git để quản lý các phiên bản mã nguồn và đẩy mã nguồn lên kho lưu trữ.
- **Trình soạn thảo mã nguồn:** Chuẩn bị trình soạn thảo chuyên nghiệp như Visual Studio Code để xem và chỉnh sửa cấu hình.
- **Tạo SSH Key Pair:** Khởi tạo trước một cặp khóa truy cập máy chủ Amazon EC2 định dạng tệp `.pem` từ bảng điều khiển AWS và lưu trữ an toàn trên máy tính cá nhân để chuẩn bị cho việc đăng nhập từ xa.

---

### 3. Kho Lưu Trữ Mã Nguồn GitHub

Chuẩn bị sẵn sàng kho lưu trữ mã nguồn cho dự án ChatPulse trên nền tảng GitHub với nhánh làm việc chính thức mang tên `main`, bao gồm hai phần cấu trúc cốt lõi:

- **Thư mục frontend:** Chứa toàn bộ giao diện người dùng viết bằng React 19, Vite, TailwindCSS.
- **Thư mục backend:** Chứa toàn bộ logic xử lý dịch vụ API và kết nối thời gian thực bằng Node.js, Express, Socket.io và TypeScript.

---

### 4. Dịch Vụ Dữ Liệu & Khóa API Bên Thứ Ba

- **Cơ sở dữ liệu MongoDB Atlas:** Đăng ký tài khoản MongoDB Atlas, tạo cụm cơ sở dữ liệu trên đám mây, cấu hình quyền truy cập mạng và lưu lại chuỗi kết nối an toàn để chuẩn bị kết nối dữ liệu người dùng và tin nhắn.
- **Dịch vụ WebRTC LiveKit:** Chuẩn bị thông tin tài khoản và lấy các thông số kết nối bao gồm địa chỉ máy chủ LiveKit SFU, API Key và Secret Key phục vụ tính năng cuộc gọi thoại và video trực tiếp.
- **Khóa API trợ lý thông minh:** Đăng ký và lấy khóa API từ Google Gemini hoặc Groq để chuẩn bị tích hợp tính năng trả lời tự động trong khung trò chuyện.

---

### 5. Đăng Ký Tên Miền Tùy Chỉnh

- **Mua tên miền chính thức:** Đăng ký và sở hữu tên miền riêng `ericmai.io.vn` thông qua nhà cung cấp dịch vụ tên miền Nhân Hòa nhằm phục vụ triển khai ứng dụng trên môi trường thực tế và gắn chứng chỉ bảo mật SSL.
- **Tài khoản quản trị DNS:** Chuẩn bị quyền quản trị tên miền tại trang dịch vụ Nhân Hòa để sẵn sàng cấu hình chuyển quyền quản lý máy chủ tên miền Name Server về cho dịch vụ Amazon Route 53.
