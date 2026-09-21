---
title: "Khó khăn và hướng phát triển"
date: 2026-06-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---


### 1. Khó Khăn Gặp Phải

Trong quá trình thiết kế và triển khai nền tảng **ChatPulse** trên AWS, dự án đối mặt với một số thách thức kỹ thuật trọng tâm:

- **Độ trễ và quá tải hệ thống thời gian thực:** Việc xử lý đồng thời luồng tin nhắn Socket.IO và luồng âm thanh, video WebRTC trên cùng máy chủ dễ gây nghẽn băng thông và quá tải tài nguyên EC2 khi lượng người dùng đồng thời tăng cao.
- **Hiện tượng lưu cache biên CDN CloudFront:** Khi phát hành bản cập nhật Frontend mới lên Amazon S3, người dùng vẫn bị trình duyệt tải lại bản giao diện cũ do chính sách lưu cache tại các điểm PoP của CloudFront, gây ra xung đột phiên bản API.
- **Bảo mật và an toàn dữ liệu phân tầng:** Cần bảo vệ an toàn tuyệt đối cho phiên đăng nhập người dùng, kiểm soát chặt chẽ quyền tải tệp tin media lên S3 và ngăn chặn các nguy cơ tấn công ứng dụng như XSS, NoSQL Injection hoặc DDoS.
- **Quản lý và kiểm soát chi phí đám mây:** Cần giám sát và tối ưu hóa tài nguyên chạy liên tục như máy chủ EC2 và ElastiCache để tránh phát sinh chi phí vượt ngoài kế hoạch trong suốt quá trình thử nghiệm.

---

### 2. Hướng Giải Quyết

Hệ thống đã áp dụng các giải pháp kỹ thuật chuẩn hóa để giải quyết triệt để từng bài toán:

- **Tách biệt kiến trúc truyền thông:** Máy chủ EC2 chỉ làm nhiệm vụ xác thực và gửi tín hiệu điều phối Signaling, đồng thời chuyển toàn bộ luồng truyền thông WebRTC qua máy chủ chuyên biệt LiveKit SFU, kết hợp Amazon ElastiCache Redis quản lý trạng thái trực tuyến và ngoại tuyến với độ trễ phản hồi cực thấp dưới 15ms.
- **Tự động hóa xóa cache CDN:** Nhúng lệnh `aws cloudfront create-invalidation` trực tiếp vào giai đoạn `post_build` trong quy trình CI/CD của AWS CodeBuild, tự động xóa sạch cache toàn cầu chỉ trong 30 đến 60 giây sau khi triển khai bản build mới.
- **Thiết lập kiến trúc bảo mật đa lớp:** Xác thực phân quyền bằng cặp token JWT gồm Access Token ngắn hạn và Refresh Token, kết hợp băm mật khẩu an toàn SHA-256, cấp quyền tải media trực tiếp lên S3 qua Pre-signed URL có chữ ký bảo mật ngắn hạn, bảo vệ an ninh mạng biên với AWS WAF và mã hóa toàn bộ dữ liệu truyền tải qua HTTPS và WSS.
- **Tối ưu chi phí và tự động dọn dẹp:** Khai thác tối đa hạn mức AWS Free Tier, cấu hình AWS Budgets gửi cảnh báo chi phí đa tầng qua email và thiết lập quy tắc S3 Lifecycle tự động dọn dẹp các tệp tin thử nghiệm sau 14 ngày.

---

### 3. Hướng Phát Triển

Để mở rộng ChatPulse thành giải pháp truyền thông cấp doanh nghiệp quy mô lớn, các định hướng phát triển tiếp theo bao gồm:

- **Container hóa với Amazon EKS:** Tái cấu trúc Backend thành các vi dịch vụ độc lập, đóng gói vào Docker và điều phối bằng Amazon EKS kết hợp AWS Fargate để tự động co giãn tài nguyên theo lưu lượng thực tế.
- **Kiến trúc đa vùng:** Mở rộng hệ thống song song tại nhiều AWS Region kết hợp định tuyến theo độ trễ thông qua Route 53 Latency-based Routing, tối ưu hóa tốc độ kết nối cho người dùng toàn cầu.
- **Tích hợp Tác Tử AI thông minh:** Ứng dụng mô hình AI từ Amazon Bedrock tự động nghe lại và tóm tắt biên bản cuộc họp video, trích xuất danh sách công việc vào phòng chat và hỗ trợ tìm kiếm ngữ nghĩa nâng cao.
- **Hiện đại hóa tầng cơ sở dữ liệu:** Chuyển đổi từ MongoDB sang các giải pháp cơ sở dữ liệu chuyên biệt trên AWS như Amazon DynamoDB để đạt hiệu năng đọc ghi quy mô lớn không máy chủ, Amazon DocumentDB nhằm tối ưu khả năng tương thích và quản trị tự động, hoặc ScyllaDB để tối đa hóa tốc độ xử lý hàng triệu tin nhắn mỗi giây với độ trễ cực thấp.
- **Bổ sung tính năng doanh nghiệp và thanh toán:** Tích hợp cổng thanh toán trực tuyến để cung cấp các gói dịch vụ nâng cao như cuộc gọi nhóm không giới hạn thời gian và dung lượng lưu trữ mở rộng.
