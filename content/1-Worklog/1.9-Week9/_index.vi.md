---
title: "Tuần 9: Tăng cường bảo mật WAF, IAM, CloudWatch và CI/CD"
date: 2026-07-20
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Chủ đề:
Thắt chặt bảo mật hệ thống với IAM Roles và AWS WAF, giám sát tập trung CloudWatch Logs và xây dựng CI/CD tự động hóa

### Mục tiêu tuần:
- Áp dụng nguyên tắc quyền tối thiểu: gán IAM Role trực tiếp cho máy chủ EC2 để thao tác với S3 và SES mà không lưu trữ thông tin xác thực cố định.
- Thiết lập tường lửa ứng dụng web AWS WAF gắn vào CloudFront để chống các kiểu tấn công web phổ biến, chặn spam bot và cấu hình Rate Limiting.
- Cấu hình CloudWatch Logs thu thập toàn bộ nhật ký hệ thống bao gồm Nginx log và Node.js log, thiết lập các Metric Filters theo dõi mã lỗi HTTP.
- Xây dựng quy trình CI/CD tự động hóa kiểm tra mã nguồn và triển khai phiên bản mới lên máy chủ EC2, thực hiện Load Testing kiểm tra năng lực chịu tải.

### Chi tiết công việc theo ngày (20/07/2026 - 24/07/2026):

| Ngày | Thứ | Nội dung công việc | Lab / Dự án thực hành |
| :--- | :--- | :--- | :--- |
| 20/07/2026 | Thứ 2 | - Tạo IAM Role ChatpulseEC2AppRole đính kèm Custom Policy cấp quyền giới hạn: s3:PutObject, s3:GetObject trên bucket media và ses:SendEmail trên verified identity.<br>- Gán IAM Role vào máy chủ EC2 qua Instance Profile.<br>- Xóa bỏ toàn bộ các biến môi trường AWS Access Key trong code backend, kiểm tra SDK tự động lấy thông tin xác thực từ EC2 Metadata Service qua IMDSv2. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 21/07/2026 | Thứ 3 | - Khởi tạo Web ACL trên AWS WAF gắn kết với CloudFront Distribution của dự án.<br>- Kích hoạt các bộ luật có sẵn của AWS: AWSManagedRulesCommonRuleSet và AWSManagedRulesKnownBadInputsRuleSet.<br>- Viết quy tắc Rate-based Rule: Giới hạn tối đa 300 requests trong vòng 5 phút trên mỗi IP nhằm ngăn chặn tấn công từ chối dịch vụ và hành vi spam tin nhắn. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 22/07/2026 | Thứ 4 | - Cấu hình CloudWatch Agent trên EC2 thu thập nhật ký từ thư mục log của PM2.<br>- Đẩy toàn bộ log lên CloudWatch Log Group aws/ec2/chatpulse/backend.<br>- Tạo Metric Filter tìm kiếm các chuỗi lỗi hoặc HTTP status 500 để phục vụ đo lường. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 23/07/2026 | Thứ 5 | - Xây dựng quy trình tự động hóa CI/CD bằng GitHub Actions.<br>- Định nghĩa file cấu hình deploy: Thực hiện lint check, chạy unit tests, build source code và tự động deploy phiên bản mới lên EC2 và khởi động lại PM2.<br>- Kiểm tra commit thử nghiệm và xác nhận quy trình CI/CD chạy thành công. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |
| 24/07/2026 | Thứ 6 | - Sử dụng công cụ kiểm thử tải giả lập 200 người dùng đồng thời gửi tin nhắn WebSocket và gọi API liên tục.<br>- Quan sát phản ứng của hệ thống: AWS WAF chặn đứng các IP vượt ngưỡng rate limit và trả về mã lỗi 429 Too Many Requests, máy chủ EC2 giữ mức CPU ổn định dưới 45%.<br>- Tổng hợp số liệu và phân tích log bảo mật tuần 9. | [Dự án cuối kỳ](https://github.com/EricMai2112/chat-pulse) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Không lưu thông tin bảo mật cố định trong mã nguồn hay máy chủ, việc sử dụng IAM Instance Profile kết hợp IMDSv2 bảo đảm an toàn dữ liệu.
  - Cơ chế phòng thủ nhiều lớp của AWS WAF: phân tích header, payload, chặn các yêu cầu độc hại ngay tại Edge Location của CloudFront trước khi chạm tới máy chủ Backend.
  - Tự động hóa quy trình CI/CD giúp tăng tốc độ phát triển và giảm thiểu rủi ro thao tác thủ công trên máy chủ sản phẩm.
- Kết quả đạt được:
  - Hệ thống backend bảo mật qua IAM Role.
  - Web ACL AWS WAF hoạt động hiệu quả, ngăn chặn thành công các request spam và request tấn công.
  - Pipeline CI/CD tự động hoạt động ổn định, nhật ký hệ thống được lưu trữ tập trung trên CloudWatch Logs.

### Khó khăn và hướng giải quyết:
- Khó khăn: Trong quá trình chạy kiểm thử tải, các yêu cầu gọi API từ máy phát triển cũng bị AWS WAF chặn do gửi yêu cầu quá dồn dập vượt ngưỡng 300 requests trong 5 phút.
- Hướng giải quyết: Cấu hình thêm IP Set trong AWS WAF chứa địa chỉ IP của máy phát triển làm danh sách cho phép, ưu tiên quy tắc này lên đầu trước khi áp dụng Rate-based Rule. Nhờ đó môi trường phát triển và kiểm thử nội bộ không bị gián đoạn.
