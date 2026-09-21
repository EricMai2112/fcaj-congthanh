---
title: "Giới thiệu"
date: 2026-06-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---


### 1. Giới Thiệu Tổng Quan

Bài thực hành này tài liệu hóa đầy đủ quy trình xây dựng và kiểm thử hệ thống hạ tầng đám mây cho dự án nền tảng nhắn tin và gọi video thời gian thực **ChatPulse** trên nền tảng **Amazon Web Services**.

Nội dung workshop tập trung vào:

- Thiết lập phân hệ mạng riêng tư bảo mật VPC với mô hình Public Subnet cho máy chủ ứng dụng và Private Subnet cho các dịch vụ dữ liệu nội bộ.
- Cấu hình máy chủ ứng dụng EC2 chạy Backend Node.js, Express và Socket.io kết hợp Nginx Reverse Proxy xử lý kết nối WebSocket thời gian thực.
- Triển khai cụm bộ nhớ đệm Amazon ElastiCache Redis nhằm quản lý trạng thái kết nối trực tuyến và phân phối tin nhắn tức thì với độ trễ thấp.
- Cấu hình lưu trữ tệp tin đa phương tiện trên Amazon S3 với cơ chế cấp quyền Pre-signed URL bảo mật ngắn hạn.
- Tối ưu hóa phân phối nội dung toàn cầu qua CloudFront, quản lý tên miền với Route 53, cấp chứng chỉ SSL từ ACM và thiết lập tường lửa AWS WAF bảo vệ mạng biên.

Thông qua quá trình thực hành thực tế này, em đã tiếp cận được phương pháp thiết kế hệ thống theo tiêu chuẩn AWS Well-Architected Framework, đặc biệt nhấn mạnh vào hai trụ cột: Bảo mật và Tối ưu hóa chi phí.

---

### 2. Sơ Đồ Kiến Trúc Hệ Thống

Toàn bộ hệ thống được triển khai tập trung tại Region Singapore ap-southeast-1:

<div style="text-align: center; margin: 24px 0;">
  <img src="/images/2-Proposal/aws-architecture.jpg" alt="Sơ đồ kiến trúc ChatPulse" style="max-width: 100%; height: auto; border-radius: 10px; box-shadow: 0 4px 16px rgba(0,0,0,0.1); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.95rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.1: Sơ đồ kiến trúc hạ tầng toàn diện bài thực hành ChatPulse trên AWS</p>
</div>

---

### 3. Thông Tin Môi Trường Thực Nghiệm

- **Domain chính thức:** [https://ericmai.io.vn](https://ericmai.io.vn)
- **AWS Region:** Region Singapore ap-southeast-1
- **Tài khoản test trải nghiệm nhanh:** `mait58674@gmail.com` / Mật khẩu: `123123`
