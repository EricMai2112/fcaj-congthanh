---
title: "Các bước triển khai"
date: 2026-06-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---


Toàn bộ quy trình triển khai hệ thống **ChatPulse** trên nền tảng **Amazon Web Services** được thực hiện tuần tự qua 7 bước kỹ thuật chuẩn hóa:

---

### Bước 1: Thiết Lập Mạng VPC, Subnet & Máy Chủ EC2 Backend

Quy trình cấu hình môi trường mạng và máy chủ tính toán cốt lõi chạy RESTful API và Engine Socket thời gian thực:

#### 1. Khởi tạo và cấu hình mạng VPC:
- Sử dụng Default VPC của khu vực Singapore ap-southeast-1 với dải mạng CIDR `172.31.0.0/16`.
- Xác định Public Subnet có bảng định tuyến Route Table liên kết với Internet Gateway để tiếp nhận lưu lượng truy cập từ Internet công cộng.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/vpc.jpg" alt="Chi tiết VPC và dải CIDR" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.3: Trang chi tiết VPC hiển thị VPC ID và dải mạng CIDR 172.31.0.0/16</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/routetables.jpg" alt="Route Table của Subnet liên kết Internet Gateway" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.4: Bảng định tuyến Route Table của Subnet liên kết với Internet Gateway</p>
</div>

#### 2. Khởi tạo máy chủ EC2 và cấu hình Elastic IP:
- Triển khai một máy chủ Amazon EC2 kích thước `t3.micro` chạy hệ điều hành Ubuntu Server trong Public Subnet (`subnet-0f379510e7e053fd0`). Đặt tên máy chủ là `ChatPulse-Backend-Server`.
- Khởi tạo và liên kết một địa chỉ IP tĩnh Elastic IP (`54.254.6.80`) trực tiếp vào máy chủ để đảm bảo địa chỉ IP công khai không bị thay đổi mỗi khi khởi động lại máy chủ.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/ec2.jpg" alt="Quản lý EC2 Instances chạy ChatPulse-Backend-Server" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.5: Trang quản lý EC2 Instances hiển thị instance ChatPulse-Backend-Server ở trạng thái Running</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/ec2details.jpg" alt="Chi tiết Instance và gắn Elastic IP tĩnh" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.6: Trang chi tiết Instance thể hiện Public IPv4 và gắn Elastic IP tĩnh 54.254.6.80</p>
</div>

#### 3. Thiết lập Security Group cho EC2:
Cấu hình Inbound Rules cho Security Group của máy chủ ứng dụng:
- **Cổng 22 (SSH):** Giới hạn truy cập quản trị hệ thống từ địa chỉ IP cá nhân của nhà phát triển.
- **Cổng 80 (HTTP) và cổng 443 (HTTPS):** Mở cho toàn bộ lưu lượng (`0.0.0.0/0`) để tiếp nhận các yêu cầu REST API và bắt tay thiết lập kết nối WebSocket WSS.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/security_groups.jpg" alt="Cấu hình Inbound Rules của Security Group" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.7: Chi tiết Security Group của EC2 với Inbound Rules mở các cổng 22, 80 và 443</p>
</div>

#### 4. Cấu hình môi trường chạy Node.js & Nginx Reverse Proxy:
- Cài đặt môi trường runtime Node.js LTS, trình quản lý tiến trình PM2 và web server Nginx trên máy chủ EC2.
- Thiết lập tệp cấu hình Nginx đóng vai trò Reverse Proxy nhận lưu lượng từ cổng 80 và 443, chuyển tiếp về ứng dụng Node.js chạy nội bộ trên cổng ứng dụng. Bật các chỉ thị `proxy_set_header Upgrade $http_upgrade` và `proxy_set_header Connection "upgrade"` để duy trì luồng dữ liệu hai chiều liên tục của Socket.IO.
- Quản lý tiến trình backend chạy nền ổn định và tự khởi động lại khi gặp lỗi thông qua PM2.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/pm2_status.jpg" alt="Trạng thái tiến trình Backend Node.js qua PM2" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.8: Màn hình Terminal chạy lệnh pm2 status hiển thị tiến trình Backend Node.js ở trạng thái online</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/nginx_status.jpg" alt="Trạng thái dịch vụ Nginx Reverse Proxy" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.9: Màn hình Terminal kiểm tra trạng thái Nginx ở trạng thái active (running)</p>
</div>

---

### Bước 2: Thiết Lập Bộ Nhớ Đệm Amazon ElastiCache & Cơ Sở Dữ Liệu MongoDB Atlas

Triển khai phân hệ lưu trữ phiên làm việc, quản lý trạng thái trực tuyến thời gian thực và kho dữ liệu cốt lõi của ứng dụng:

#### 1. Khởi tạo cụm Amazon ElastiCache Redis:
- Khởi tạo cụm ElastiCache Redis với node type `cache.t3.micro` đặt trong phân vùng mạng VPC nội bộ.
- Thiết lập Security Group cho ElastiCache chỉ chấp nhận lưu lượng TCP trên cổng mặc định `6379` xuất phát từ Security Group của máy chủ EC2 Backend.
- Tích hợp Redis Client trong mã nguồn Node.js để lưu trữ danh sách Socket ID, quản lý Room chat và cập nhật trạng thái hoạt động người dùng (Presence: Online, Offline, Typing) với tốc độ phản hồi tính bằng mili-giây.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/elasticache.jpg" alt="Quản lý ElastiCache Redis" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.10: Trang quản lý Amazon ElastiCache hiển thị cụm Redis ở trạng thái Available</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/elasticache_details.jpg" alt="Chi tiết kết nối Endpoint của cụm Redis" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.11: Trang chi tiết cụm Redis hiển thị Endpoint kết nối nội bộ và cổng 6379</p>
</div>

#### 2. Liên kết cơ sở dữ liệu MongoDB Atlas:
- Cấu hình Network Access trên MongoDB Atlas cho phép địa chỉ IP tĩnh Elastic IP của EC2 (`54.254.6.80`) truy cập thông qua Database User được phân quyền cụ thể.
- Quản lý các collection dữ liệu chính gồm Users, Conversations, Messages phục vụ việc lưu trữ lịch sử hội thoại lâu dài và hồ sơ tài khoản người dùng.

---

### Bước 3: Thiết Lập Lưu Trữ Tĩnh Amazon S3, Định Tuyến Route 53 & Chứng Chỉ SSL ACM

Quy trình chuẩn bị kho lưu trữ phân phối tĩnh và lớp bảo mật mã hóa đường truyền:

#### 1. Khởi tạo Amazon S3 Bucket:
- Tạo một S3 Bucket riêng biệt để lưu trữ mã nguồn đóng gói Frontend (`dist/`) của ứng dụng web.
- Thiết lập cấu hình cấp quyền riêng tư với Origin Access Control (OAC) để chỉ cho phép phân phối thông qua Amazon CloudFront, chặn toàn bộ truy cập trực tiếp từ bên ngoài.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/s3.jpg" alt="Cấu hình Amazon S3 Bucket chứa mã nguồn tĩnh Frontend" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.12: Trang quản trị Amazon S3 Bucket lưu trữ mã nguồn tĩnh Frontend của dự án</p>
</div>

#### 2. Cấu hình tên miền trên Amazon Route 53:
- Kiểm tra thông tin kích hoạt tên miền `ericmai.io.vn` tại nhà đăng ký Nhân Hòa:

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/domain.jpg" alt="Trạng thái tên miền ericmai.io.vn tại Nhân Hòa" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.13: Quản trị dịch vụ tại Nhân Hòa hiển thị tên miền ericmai.io.vn ở trạng thái hoạt động</p>
</div>

- Cấu hình chuyển quyền quản lý máy chủ tên miền Name Server từ Nhân Hòa trỏ về các máy chủ DNS của Amazon Route 53:

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/name_server_dns.jpg" alt="Cấu hình Name Server trên trang quản lý Nhân Hòa" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.14: Cấu hình bản ghi Name Server tại Nhân Hòa trỏ về 4 máy chủ DNS của Route 53</p>
</div>

- Khởi tạo Public Hosted Zone cho tên miền chính `ericmai.io.vn` và cấu hình các bản ghi DNS cốt lõi:
  - **Bản ghi Record A (Alias):** Trỏ tên miền chính `ericmai.io.vn` về địa chỉ phân phối của CloudFront CDN.
  - **Bản ghi Record A (Subdomain Backend):** Trỏ tên miền phụ `api.ericmai.io.vn` về địa chỉ IP tĩnh Elastic IP của máy chủ EC2 (`54.254.6.80`).

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/route53.jpg" alt="Cấu hình bản ghi DNS trên Amazon Route 53" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.15: Trang chi tiết Route 53 Hosted Zone hiển thị danh sách các bản ghi DNS định tuyến tên miền</p>
</div>

#### 3. Cấp phát chứng chỉ SSL với AWS Certificate Manager (ACM):
- Gửi yêu cầu cấp phát chứng chỉ SSL/TLS công khai (Wildcard Certificate cho `*.ericmai.io.vn` và `ericmai.io.vn`) tại Region US East N. Virginia (`us-east-1`) để tương thích với dịch vụ Amazon CloudFront.
- Thực hiện xác thực quyền sở hữu tên miền thông qua bản ghi DNS CNAME tự động liên kết với Route 53.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/acm.jpg" alt="Cấp phát chứng chỉ SSL trên AWS Certificate Manager" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.16: Quản lý chứng chỉ AWS Certificate Manager hiển thị chứng chỉ SSL ở trạng thái Issued</p>
</div>

---

### Bước 4: Cấu Hình Phân Phối CloudFront & Tường Lửa Ứng Dụng AWS WAF

Thiết lập mạng lưới phân phối biên toàn cầu kết hợp lớp phòng vệ an ninh mạng:

#### 1. Thiết lập Amazon CloudFront Distribution:
- Tạo một phân phối CloudFront mới, trỏ Origin chính về S3 Bucket chứa mã nguồn tĩnh Frontend.
- Đính kèm chứng chỉ SSL/TLS từ ACM để kích hoạt giao thức HTTPS trên toàn bộ Edge Locations toàn cầu.
- Cấu hình Alternate Domain Names (CNAMEs) trùng khớp với tên miền đã thiết lập trên Route 53 (`ericmai.io.vn`).
- Cài đặt Custom Error Responses (chuyển hướng mã lỗi 403 và 404 về `/index.html` với mã phản hồi HTTP `200 OK`) để hỗ trợ cơ chế định tuyến Client-side Routing của Single Page Application (React Router).

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/cloudfront.jpg" alt="Cấu hình phân phối Amazon CloudFront" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.17: Trang quản lý Amazon CloudFront hiển thị phân phối CDN ở trạng thái hoạt động (Enabled)</p>
</div>

#### 2. Kích hoạt tường lửa ứng dụng AWS WAF:
- Khởi tạo một Web ACL trong AWS WAF và liên kết trực tiếp với CloudFront Distribution.
- Kích hoạt các bộ quy tắc bảo mật được quản lý bởi AWS (AWS Managed Rules) gồm: `AWSManagedRulesCommonRuleSet` và `AWSManagedRulesKnownBadInputsRuleSet` nhằm ngăn chặn các hành vi tấn công DDoS tầng ứng dụng (Layer 7), Cross-Site Scripting (XSS), SQLi và quét cổng tự động.

---

### Bước 5: Cấu Hình Dịch Vụ Trợ Năng Amazon Polly & Dịch Vụ Email Amazon SES

Tích hợp các dịch vụ đám mây chuyên dụng phục vụ tính năng nghiệp vụ của hệ thống:

#### 1. Thiết lập Amazon Simple Email Service (SES):
- Thêm và xác minh danh tính tên miền (Domain Identity) hoặc địa chỉ email gửi trên Amazon SES.
- Cấu hình xác thực bản ghi SPF và DKIM trên Route 53 để nâng cao độ tin cậy và đảm bảo email không bị chuyển vào thư rác.
- Tích hợp AWS SDK trong Backend để tự động gửi email xác thực tài khoản đăng ký mới và gửi mã OTP khôi phục mật khẩu.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/ses_gmail.jpg" alt="Xác thực email gửi trên Amazon SES" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.18: Trang quản lý Amazon SES hiển thị danh tính email gửi đã được xác thực (Verified)</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/received_gmail.jpg" alt="Hộp thư nhận email OTP khôi phục mật khẩu" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.19: Hộp thư Gmail nhận email gửi mã OTP khôi phục mật khẩu (quên mật khẩu) tự động từ hệ thống ChatPulse qua SES</p>
</div>

#### 2. Tích hợp tính năng Text-to-Speech với Amazon Polly:
- Phân quyền gọi API Amazon Polly thông qua IAM Role và AWS SDK trên máy chủ backend.
- Triển khai endpoint cho phép chuyển đổi nội dung tin nhắn dạng văn bản sang giọng đọc audio tự nhiên (định dạng mp3) phục vụ tính năng trợ năng nghe tin nhắn trực tiếp trong phòng chat.

---

### Bước 6: Xây Dựng Pipeline Tự Động Hóa CI/CD Với AWS CodePipeline & AWS CodeBuild

Tự động hóa toàn bộ quy trình phát hành từ khâu đẩy mã nguồn đến khâu triển khai bản build mới lên CDN:

#### 1. Cấu hình AWS CodeBuild:
- Tạo một Build Project mới trên CodeBuild với môi trường container Linux (Ubuntu tiêu chuẩn, Node.js runtime).
- Tạo tệp `buildspec.yml` đặt tại thư mục gốc của frontend, định nghĩa các giai đoạn:
  - **install:** Cài đặt các gói thư viện phụ thuộc (`npm install`).
  - **build:** Nhúng các biến môi trường và đóng gói ứng dụng React/Vite (`npm run build`).
  - **post_build:** Tự động đồng bộ thư mục tĩnh lên S3 bằng lệnh `aws s3 sync dist/ s3://<bucket-name> --delete`, đồng thời kích hoạt lệnh xóa cache toàn cầu trên CloudFront:
    ```bash
    aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
    ```
- Cấp quyền IAM Role cho CodeBuild để ghi dữ liệu vào S3 Bucket và thực thi lệnh Invalidation trên CloudFront.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/codebuild.jpg" alt="Cấu hình dự án trên AWS CodeBuild" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.20: Giao diện quản lý dự án AWS CodeBuild hiển thị cấu hình môi trường và lịch sử thực thi</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/buildspec.jpg" alt="Nội dung tệp cấu hình buildspec.yml" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.21: Cấu trúc nội dung tệp buildspec.yml định nghĩa các giai đoạn đóng gói và triển khai</p>
</div>

#### 2. Thiết lập luồng tự động với AWS CodePipeline:
- Khởi tạo CodePipeline liên kết trực tiếp với GitHub Repository thông qua kết nối GitHub Webhook, tự động kích hoạt mỗi khi có commit mới được merge vào nhánh `main`.
- Kết nối Source Stage (GitHub) với Build Stage (AWS CodeBuild).
- Khi lập trình viên thực hiện thao tác `git push`, toàn bộ quá trình đóng gói, tải file lên S3 và xóa cache CloudFront được thực thi tự động mà không cần can thiệp thủ công.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/pipeline.jpg" alt="Luồng CI/CD trên AWS CodePipeline" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.22: Luồng CI/CD AWS CodePipeline với các giai đoạn Source và Build hoàn thành ở trạng thái Succeeded</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/pipeline_details.jpg" alt="Chi tiết các bước thực thi trong CodePipeline" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.23: Chi tiết nhật ký thực thi và các bước triển khai tự động trong AWS CodePipeline</p>
</div>

---

### Bước 7: Cấu Hình Giám Sát & Cảnh Báo Với Amazon CloudWatch

Thiết lập hệ thống theo dõi sức khỏe phần cứng máy chủ và trạng thái ứng dụng theo thời gian thực:

#### 1. Cài đặt và cấu hình CloudWatch Agent trên EC2:
- Gán IAM Role `EC2-CloudWatchAgent-Role` cho máy chủ EC2 để cấp quyền gửi các số liệu giám sát và nhật ký hoạt động về CloudWatch.
- Cấu hình thu thập liên tục các chỉ số tài nguyên phần cứng cốt lõi gồm: Tỷ lệ sử dụng CPU (CPU Utilization), dung lượng bộ nhớ RAM khả dụng và lưu lượng mạng Inbound/Outbound.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/ec2_cloudwatch.jpg" alt="Biểu đồ CloudWatch Metrics giám sát máy chủ EC2" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.24: Biểu đồ theo dõi các chỉ số tài nguyên máy chủ EC2 (CPU Utilization, Network) trên Amazon CloudWatch</p>
</div>

#### 2. Thiết lập Cảnh báo tự động (CloudWatch Alarms):
- Khởi tạo cảnh báo ngưỡng tài nguyên: Kích hoạt trạng thái ALARM khi tỷ lệ sử dụng CPU của EC2 vượt ngưỡng 80% liên tục trong vòng 5 phút.
- Liên kết hành động cảnh báo với Amazon SNS để gửi email cảnh báo tức thời cho quản trị viên khi hệ thống có dấu hiệu quá tải.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/cloudwatch_alarm.jpg" alt="Trang quản lý cảnh báo CloudWatch Alarms" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.25: Trang quản lý CloudWatch Alarms hiển thị cấu hình cảnh báo giám sát ngưỡng tài nguyên hệ thống</p>
</div>
