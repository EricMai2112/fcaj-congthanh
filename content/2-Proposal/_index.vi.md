---
title: "Bản đề xuất"
date: 2026-06-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# ChatPulse – Nền tảng Nhắn tin & Gọi Video Real-time Triển khai Hạ tầng AWS Cloud
### Giải pháp truyền thông thời gian thực bảo mật, tích hợp AI và tự động hóa CI/CD trên nền tảng Amazon Web Services

---

### 1. Tóm Tắt Dự Án

**ChatPulse** là nền tảng truyền thông thời gian thực trên nền tảng Web, cho phép người dùng dễ dàng kết nối bạn bè, tạo nhóm trò chuyện, nhắn tin tức thì, gọi thoại và gọi video chất lượng cao, tích hợp trợ năng giọng nói thông minh và hệ thống bảo mật đa tầng từ xác thực JWT, băm mật khẩu SHA-256 đến bảo vệ biên AWS WAF.

Toàn bộ hệ thống được thiết kế, triển khai và vận hành trực tiếp trên hạ tầng điện toán đám mây **Amazon Web Services** tại Region Singapore ap-southeast-1, tuân thủ các nguyên tắc thiết kế của **AWS Well-Architected Framework**. Dự án áp dụng quy trình tích hợp và phân phối liên tục CI/CD tự động, đảm bảo quá trình phát hành phiên bản mới diễn ra nhanh chóng, an toàn và ổn định.

- **🌐 Live Demo:** [https://ericmai.io.vn](https://ericmai.io.vn)

---

### 2. Mục Tiêu Dự Án

Dự án ChatPulse được xây dựng nhằm đạt được các mục tiêu trọng tâm sau:

1. **Xây dựng nền tảng giao tiếp thời gian thực:** Cung cấp trải nghiệm kết nối bạn bè, tạo nhóm trò chuyện, gửi nhận tin nhắn tức thì với độ trễ thấp và gọi thoại, video chất lượng cao, mượt mà trên trình duyệt web.
2. **Bảo mật hệ thống và an toàn dữ liệu:** Triển khai cơ chế xác thực phân quyền qua JWT, băm mật khẩu một chiều an toàn bằng SHA-256, kiểm duyệt chặt chẽ dữ liệu đầu vào chống NoSQL Injection, XSS, mã hóa toàn bộ lưu lượng qua HTTPS, WSS và thiết lập tường lửa AWS WAF bảo vệ tầng ứng dụng.
3. **Tích hợp tính năng AI và trợ năng thông minh:** Ứng dụng mô hình AI hỗ trợ gợi ý hội thoại và sử dụng dịch vụ Amazon Polly để chuyển văn bản thành giọng đọc tự nhiên, hỗ trợ người dùng thuận tiện hơn.
4. **Triển khai hạ tầng đám mây chuẩn AWS:** Thiết kế kiến trúc phân tầng an toàn trong mạng VPC, tối ưu hóa hiệu năng bộ nhớ đệm với Amazon ElastiCache Redis, bảo vệ an ninh mạng biên bằng AWS WAF và phân phối nội dung qua Amazon CloudFront.
5. **Tự động hóa quy trình triển khai:** Thiết lập quy trình CI/CD tự động đóng gói và cập nhật ứng dụng lên hạ tầng AWS, đảm bảo phát hành phiên bản mới nhanh chóng và không gây gián đoạn dịch vụ.

---

### 3. Vấn Đề Cần Giải Quyết & Giá Trị Mang Lại

- **Thực trạng:** Nhu cầu liên lạc trực tuyến ngày càng lớn, tuy nhiên nhiều nền tảng trò chuyện hiện nay vẫn lưu trữ dữ liệu thiếu cơ chế kiểm soát chặt chẽ hoặc dùng quy trình xác thực đơn giản, tiềm ẩn nguy cơ lộ lọt thông tin cá nhân. Bên cạnh đó, hệ thống dễ gặp hiện tượng nghẽn mạng khi lượng người dùng đồng thời tăng cao, quy trình cập nhật phần mềm thủ công thường gây gián đoạn dịch vụ và các tính năng trợ năng âm thanh cho người dùng còn nhiều hạn chế.
- **Giải pháp:** ChatPulse xây dựng giải pháp truyền thông hiện đại với kiến trúc bảo mật đa tầng, bao gồm băm mật khẩu an toàn với SHA-256, xác thực phân quyền nghiêm ngặt với cặp token JWT, kiểm duyệt dữ liệu đầu vào qua express-validator và phân quyền tải media qua S3 Pre-signed URL. Hệ thống ứng dụng cụm bộ nhớ đệm Amazon ElastiCache Redis nhằm tối ưu hóa việc quản lý trạng thái kết nối và phân phối tin nhắn tức thì, kết hợp công nghệ WebRTC SFU cho cuộc gọi chất lượng cao, tích hợp Amazon Polly hỗ trợ giọng đọc thông minh, mã hóa toàn bộ dữ liệu truyền tải qua HTTPS, WSS và thiết lập tường lửa AWS WAF bảo vệ biên.
- **Lợi ích:** Mang đến cho người dùng một không gian kết nối bạn bè và làm việc nhóm an toàn, bảo mật và mượt mà, tối ưu hóa tài nguyên và chi phí vận hành cho hệ thống, đồng thời đảm bảo nền tảng luôn vận hành liên tục, ổn định và sẵn sàng mở rộng trong tương lai.

---

### 4. Kiến Trúc Hệ Thống & Công Nghệ Sử Dụng

#### Sơ đồ kiến trúc tổng thể trên AWS

Toàn bộ kiến trúc hệ thống ChatPulse được thiết kế và triển khai trên hạ tầng điện toán đám mây Amazon Web Services tại Region Singapore ap-southeast-1, tuân thủ mô hình mạng VPC phân tầng bảo mật gồm Public Subnet cho máy chủ ứng dụng và Private Subnet cho các dịch vụ dữ liệu nội bộ.

<div style="text-align: center; margin: 24px 0;">
  <img src="/images/2-Proposal/aws-architecture.jpg" alt="Sơ đồ kiến trúc nền tảng ChatPulse trên AWS Cloud" style="max-width: 100%; height: auto; border-radius: 10px; box-shadow: 0 4px 20px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.95rem; color: #64748b; margin-top: 10px; font-weight: 500; font-style: italic;">Hình 1: Sơ đồ kiến trúc hạ tầng toàn diện của ChatPulse trên nền tảng Amazon Web Services tại Region Singapore ap-southeast-1</p>
</div>

#### Bảng công nghệ sử dụng

| Phân tầng | Công nghệ / Dịch vụ | Vai trò & Mục đích sử dụng |
| :--- | :--- | :--- |
| **Frontend Client** | React 19, Vite, TypeScript | Xây dựng giao diện web phản hồi nhanh, tối ưu hóa kích thước bundle. |
| | TailwindCSS v4, Radix UI | Thiết kế giao diện hiện đại, hỗ trợ Dark/Light mode, chuẩn responsive. |
| | Zustand, TanStack Query v5 | Quản lý trạng thái ứng dụng toàn cục và tối ưu hóa truy vấn dữ liệu client. |
| | Socket.io-client, LiveKit-client | Thiết lập kênh giao tiếp hai chiều WebSocket và truyền dẫn media WebRTC. |
| **Backend API** | Node.js, Express, TypeScript | Xây dựng RESTful API và dịch vụ điều phối thời gian thực với hiệu năng cao. |
| | Socket.io Server, PM2 | Xử lý hàng nghìn kết nối đồng thời, tự động hồi phục khi xảy ra ngoại lệ. |
| | LiveKit Server SDK | Điều phối phòng gọi thoại, video độ trễ thấp theo mô hình SFU. |
| **Cơ sở dữ liệu** | MongoDB Native Driver | Lưu trữ thông tin tài khoản, danh bạ bạn bè, nhóm trò chuyện và tin nhắn. |
| | **Amazon ElastiCache Redis** | Quản lý trạng thái online/offline, rate limit và bộ nhớ đệm phiên làm việc. |
| **Bảo mật & Mạng** | **Amazon Route 53** | Quản lý bản ghi DNS, điều phối tên miền `ericmai.io.vn` và subdomain API. |
| | **AWS Certificate Manager** | Cung cấp chứng chỉ SSL/TLS miễn phí, bảo mật truyền thông HTTPS và WSS. |
| | **AWS WAF** | Ngăn chặn tấn công lớp ứng dụng như SQLi, XSS, DDoS và giới hạn tần suất truy cập. |
| | **Amazon CloudFront** | Mạng phân phối nội dung toàn cầu, giảm thiểu độ trễ tải trang web. |
| **Điện toán & Lưu trữ**| **Amazon EC2** | Máy chủ ứng dụng chạy Backend Node.js kết hợp Nginx Reverse Proxy. |
| | **Amazon S3** | Lưu trữ mã nguồn tĩnh Frontend và tệp tin đa phương tiện người dùng tải lên. |
| **AI & Dịch vụ phụ trợ**| **Amazon Polly** | Dịch vụ Text-to-Speech tổng hợp tin nhắn văn bản thành giọng đọc tự nhiên. |
| | **Amazon SES** | Cổng gửi email xác thực tài khoản, mã OTP và thông báo hệ thống. |
| | Gemini AI & Groq SDK | Cung cấp năng lực phản hồi ngữ cảnh thông minh trong khung chat. |
| **DevOps & Giám sát** | **AWS CodePipeline & CodeBuild** | Xây dựng quy trình tự động CI/CD cho Frontend khi có mã nguồn mới. |
| | **Amazon CloudWatch** | Giám sát tài nguyên máy chủ EC2 và phát cảnh báo tự động qua CloudWatch Alarms. |

---

### 5. Triển Khai Kỹ Thuật

#### Các giai đoạn thực hiện:
- **Nghiên cứu và thiết kế:** Phân tích yêu cầu, thiết kế kiến trúc hệ thống theo Well-Architected Framework, thiết kế cơ sở dữ liệu và API endpoints.
- **Phát triển Backend:** Xây dựng RESTful API và WebSocket với Node.js, Express, tích hợp xác thực JWT, kết nối MongoDB, cấu hình ElastiCache Redis và LiveKit WebRTC.
- **Phát triển Frontend:** Xây dựng giao diện Web bằng React 19 và Vite, thiết kế responsive với TailwindCSS, tích hợp chatbot AI và chuyển văn bản thành giọng nói qua Amazon Polly.
- **Triển khai và kiểm thử:** Triển khai hệ thống lên AWS, cấu hình tường lửa AWS WAF, thiết lập luồng CI/CD tự động và kiểm thử toàn diện.

#### Yêu cầu kỹ thuật:
- **Backend:** Node.js, Express, TypeScript, Socket.io, LiveKit Server SDK.
- **Frontend:** React 19, Vite, TailwindCSS, Zustand, Socket.io-client.
- **Cơ sở dữ liệu & Cache:** MongoDB, Amazon ElastiCache Redis.
- **Hạ tầng AWS:** VPC, EC2, S3, CloudFront, Route 53, CloudWatch, CodePipeline.
- **Bảo mật:** AWS WAF, SSL/TLS, JWT, băm mật khẩu SHA-256, S3 Pre-signed URL.

---

### 6. Lộ Trình Triển Khai

- **Tuần 1–5: 25/05 – 26/06:** Nghiên cứu và thực hành chuỗi lab nền tảng AWS: IAM, VPC, EC2, S3, RDS, DynamoDB, Serverless, Docker, CloudFront và Route 53.
- **Tuần 6: 29/06 – 03/07:** Khởi động dự án ChatPulse, phân tích yêu cầu, thiết kế kiến trúc Well-Architected, thiết lập mạng VPC và S3 Media Bucket.
- **Tuần 7: 06/07 – 10/07:** Khởi tạo cấu trúc mã nguồn, phát triển Backend Auth với JWT, băm mật khẩu SHA-256, gửi email OTP qua Amazon SES và dựng ElastiCache Redis.
- **Tuần 8: 13/07 – 17/07:** Xây dựng chat thời gian thực với Socket.io, gọi video LiveKit WebRTC, tải file lên S3 qua Pre-signed URL và gắn chứng chỉ SSL qua ACM.
- **Tuần 9: 20/07 – 24/07:** Phân quyền IAM Role, cấu hình tường lửa AWS WAF, giám sát CloudWatch Logs và xây dựng luồng CI/CD tự động qua CodePipeline.
- **Tuần 10: 27/07 – 31/07:** Hoàn thiện giao diện Web React 19 và Vite, tích hợp AI và Amazon Polly, kiểm thử toàn diện hệ thống và quay video demo.
- **Tuần 11: 03/08 – 07/08:** Tối ưu hóa chi phí đám mây với S3 Lifecycle, đo lường hiệu năng hệ thống và viết 5 bài blog kỹ thuật trên AWS Study Group.
- **Tuần 12: 10/08 – 14/08:** Hoàn thiện các tính năng, tối ưu mã nguồn, hoàn thành báo cáo thực tập song ngữ và nghiệm thu dự án.

---

### 7. Ước Tính Ngân Sách & Tối Ưu Chi Phí

Chi phí hạ tầng hàng tháng được tính toán chi tiết bằng công cụ **[AWS Pricing Calculator](https://calculator.aws/)** cho Region Singapore ap-southeast-1, dựa trên định mức vận hành 730 giờ/tháng phục vụ quy mô thử nghiệm và vận hành thực tế:

| Dịch vụ AWS | Cấu hình kỹ thuật chi tiết | Chi phí ước tính (USD/tháng) | Ghi chú tối ưu chi phí |
| :--- | :--- | :---: | :--- |
| **Amazon EC2** | 1 instance t3.small, 2 vCPU, 2GB RAM, 30GB EBS gp3 | **15.20 USD** | Chạy Backend Node.js, Socket.IO và Nginx. Áp dụng gói Savings Plans khi chạy lâu dài. |
| **Amazon ElastiCache** | 1 node cache.t3.micro Redis OSS Private Subnet | **18.25 USD** | Quản lý trạng thái kết nối và bộ nhớ đệm phiên làm việc với độ trễ thấp. |
| **AWS WAF** | 1 Web ACL, 3 Core Managed Rule Groups, 10 triệu requests/tháng | **6.50 USD** | Bảo vệ hệ thống khỏi tấn công DDoS và lọc lưu lượng độc hại ngay tại biên. |
| **Amazon CloudFront** | Phân phối nội dung CDN toàn cầu, khoảng 50GB data transfer out | **0.00 USD** | Nằm hoàn toàn trong gói AWS Free Tier với 1TB Data Transfer mỗi tháng. |
| **Amazon S3** | S3 Standard, khoảng 10GB lưu trữ web bundle và ảnh tải lên | **0.25 USD** | Thiết lập S3 Lifecycle Rules chuyển dữ liệu cũ sang Glacier để tiết kiệm chi phí. |
| **Amazon Route 53** | 1 Hosted Zone `ericmai.io.vn` và 1 triệu truy vấn DNS/tháng | **0.90 USD** | Chi phí cố định cho quản lý DNS tên miền chính thức. |
| **Amazon SES** | Gửi khoảng 2.000 email thông báo và mã OTP/tháng | **0.00 USD** | Nằm trong định mức miễn phí 62.000 email/tháng khi gửi từ ứng dụng chạy trên Amazon EC2. |
| **Amazon Polly** | Chuyển đổi khoảng 50.000 ký tự văn bản thành giọng đọc tự nhiên/tháng | **0.00 USD** | Nằm trong AWS Free Tier miễn phí 5 triệu ký tự văn bản mỗi tháng. |
| **AWS CodePipeline** | 1 Active Pipeline với nguồn từ GitHub | **0.00 USD** | Nằm trong Free Tier miễn phí 1 active pipeline mỗi tháng. |
| **AWS CodeBuild** | Khoảng 60 phút build/tháng sử dụng cấu hình general1.small | **0.00 USD** | Nằm trong Free Tier miễn phí 100 phút build mỗi tháng. |
| **Amazon CloudWatch** | 5 Custom Metrics, 3 Cảnh báo Alarms, 2GB Logs lưu trữ | **2.10 USD** | Tối ưu thời gian lưu log xuống 14 ngày để không phát sinh chi phí lưu trữ dư thừa. |
| **TỔNG CỘNG HÀNG THÁNG** | *Duy trì toàn bộ hệ thống Production* | **~43.20 USD / tháng** | *~518.40 USD / năm* |

---

### 8. Đánh Giá Rủi Ro & Phương Án Dự Phòng

#### Ma trận rủi ro:
- **Quá tải kết nối WebSocket:** Mức độ ảnh hưởng cao, xác suất trung bình khi lượng người dùng đồng thời tăng đột biến.
- **Tấn công từ chối dịch vụ DDoS hoặc XSS:** Mức độ ảnh hưởng cao, xác suất trung bình tại tầng ứng dụng và mạng biên.
- **Rò rỉ hoặc đánh cắp Token xác thực JWT:** Mức độ ảnh hưởng cao, xác suất thấp nếu không có cơ chế thu hồi tức thì.
- **Vượt ngân sách dự toán AWS:** Mức độ ảnh hưởng trung bình, xác suất thấp khi tài nguyên nhàn rỗi không được dọn dẹp.
- **Lỗi lưu cache trình duyệt cũ sau deploy:** Mức độ ảnh hưởng trung bình, xác suất cao do CDN giữ bản build cũ.

#### Chiến lược giảm thiểu:
- **Tối ưu kết nối và truyền dẫn:** Phân tải trạng thái người dùng qua cụm Amazon ElastiCache Redis, điều phối luồng gọi video qua máy chủ LiveKit SFU riêng biệt, cấu hình Nginx giữ kết nối Keep-Alive.
- **Bảo mật mạng biên và dữ liệu:** Kích hoạt AWS WAF chặn IP độc hại, thiết lập giới hạn Rate Limit 30 requests/giây cho mỗi IP, mã hóa dữ liệu truyền tải qua HTTPS và WSS, phân quyền tải media qua S3 Pre-signed URL.
- **Quản lý phiên làm việc an toàn:** Thiết lập Access Token thời hạn ngắn 15 phút, lưu trữ và quản lý Refresh Token chặt chẽ trong database, lập tức thu hồi token khi người dùng đăng xuất.
- **Kiểm soát chi phí:** Cấu hình AWS Budgets gửi email cảnh báo chi phí qua Amazon SNS theo các mốc 15 USD, 30 USD và 40 USD, thiết lập S3 Lifecycle tự động chuyển dữ liệu cũ sang Glacier.

#### Kế hoạch dự phòng:
- **Tự động làm mới cache CDN:** Nhúng lệnh xóa cache CloudFront tự động trong kịch bản CodeBuild ngay sau khi tải bản build mới lên S3.
- **Khôi phục nhanh phiên bản ổn định:** Sử dụng pipeline CI/CD để thực hiện rollback về bản dựng ổn định trước đó khi phát hiện lỗi nghiêm trọng.
- **Sao lưu và phục hồi dữ liệu:** Thiết lập chính sách sao lưu định kỳ cho cơ sở dữ liệu và cấu hình hạ tầng để sẵn sàng khôi phục khi có sự cố.

---

### 9. Kết Quả Kỳ Vọng

#### Cải tiến kỹ thuật:
- Hoàn thiện nền tảng ChatPulse vận hành trực tuyến mượt mà tại địa chỉ [https://ericmai.io.vn](https://ericmai.io.vn) với đầy đủ các tính năng truyền thông thời gian thực:
  - **Kết nối và tương tác bạn bè:** Tìm kiếm người dùng, gửi và nhận lời mời kết bạn, quản lý danh sách bạn bè, theo dõi trạng thái online và offline theo thời gian thực.
  - **Hội thoại cá nhân và nhóm:** Tạo nhóm trò chuyện linh hoạt, quản lý quyền hạn thành viên, nhắn tin tức thì với độ trễ thấp, chia sẻ hình ảnh và tệp tài liệu an toàn qua Amazon S3.
  - **Cuộc gọi thời gian thực và trợ năng AI:** Thực hiện cuộc gọi thoại và video call chất lượng cao qua công nghệ WebRTC SFU, tích hợp trợ năng chuyển văn bản thành giọng nói thông minh qua Amazon Polly và trợ lý AI hội thoại.
- Xây dựng kiến trúc điện toán đám mây phân tầng bảo mật cao, tuân thủ 6 trụ cột của AWS Well-Architected Framework, sẵn sàng mở rộng và đạt hiệu suất cao với độ trễ thấp.
- Tự động hóa toàn diện quy trình đóng gói và phát hành ứng dụng với luồng CI/CD qua AWS CodePipeline và AWS CodeBuild.

#### Giá trị thực tiễn và dài hạn:
- Mang lại môi trường giao tiếp an toàn, bảo mật thông tin cá nhân và dữ liệu người dùng qua cơ chế xác thực JWT, băm mật khẩu SHA-256 và bảo vệ biên AWS WAF.
- Tối ưu hóa chi phí vận hành ở mức tiết kiệm và hiệu quả, tận dụng tối đa gói AWS Free Tier, phù hợp cho quy mô thử nghiệm và phát triển mở rộng trong tương lai.
- Tạo tiền đề kỹ thuật vững chắc để tiếp tục tích hợp thêm các dịch vụ AI và các tính năng tương tác đa phương tiện nâng cao.