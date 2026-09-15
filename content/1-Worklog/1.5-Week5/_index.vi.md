---
title: "Tuần 5: Container Docker, ECR, CloudFront và Route 53"
date: 2026-06-22
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Chủ đề:
Đóng gói ứng dụng Container với Docker và Amazon ECR, phân phối nội dung toàn cầu với Amazon CloudFront và quản lý tên miền Amazon Route 53

### Mục tiêu tuần:
- Làm chủ kỹ thuật đóng gói ứng dụng bằng Docker: viết Dockerfile đa tầng nhằm giảm thiểu dung lượng image và tăng cường bảo mật runtime.
- Khởi tạo kho chứa riêng biệt Amazon Elastic Container Registry, thực hiện xác thực và đẩy Docker Container Image lên đám mây AWS.
- Thiết lập hệ thống quản lý tên miền với Amazon Route 53: cấu hình Public Hosted Zone và các loại bản ghi DNS.
- Cấu hình mạng phân phối nội dung Amazon CloudFront: tối ưu hóa tốc độ tải trang qua bộ nhớ đệm tại các Edge Location và cấu hình bảo mật Origin Access Control.

### Chi tiết công việc theo ngày (22/06/2026 - 26/06/2026):

| Ngày | Thứ | Nội dung công việc | Lab / Dự án thực hành | Nguồn tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| 22/06/2026 | Thứ 2 | - Nghiên cứu công nghệ Containerization và sự khác biệt giữa Container và Virtual Machine.<br>- Viết Dockerfile theo chuẩn Multi-stage build cho một ứng dụng mẫu Node.js và React.<br>- Tối ưu hóa file dockerignore, build image cục bộ và kiểm tra tính năng bằng docker run. | Xây dựng Production Containers dung lượng nhẹ với Docker | [Docker Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) |
| 23/06/2026 | Thứ 3 | - Tìm hiểu dịch vụ lưu trữ container Amazon Elastic Container Registry.<br>- Tạo Private Repository fcaj-sample-app trên Amazon ECR và kích hoạt tính năng quét lỗ hổng bảo mật khi đẩy image.<br>- Lấy token xác thực bằng AWS CLI qua lệnh aws ecr get-login-password, gắn tag image và đẩy container image lên ECR. | Đẩy Docker Image an toàn lên Amazon ECR Private Repository | [Amazon ECR User Guide](https://docs.aws.amazon.com/AmazonECR/latest/userguide/) |
| 24/06/2026 | Thứ 4 | - Tìm hiểu dịch vụ DNS Amazon Route 53: nguyên lý phân giải tên miền, các loại DNS records và chính sách định tuyến Routing policies.<br>- Khởi tạo Public Hosted Zone trong Route 53.<br>- Thực hành cấu hình các bản ghi: Record A trỏ về IP máy chủ, CNAME và bản ghi Alias của AWS. | Quản lý tên miền và định tuyến DNS với Amazon Route 53 | [Amazon Route 53 Documentation](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/) |
| 25/06/2026 | Thứ 5 | - Nghiên cứu cơ chế hoạt động của mạng phân phối nội dung Amazon CloudFront gồm Edge Locations, Regional Edge Caches và Origins.<br>- Tạo CloudFront Distribution trỏ Origin tới S3 Static Website Bucket.<br>- Cấu hình Origin Access Control và cập nhật S3 Bucket Policy để chỉ cho phép duy nhất CloudFront đọc dữ liệu. | Tăng tốc phân phối nội dung toàn cầu với CloudFront và bảo vệ Origin | [Amazon CloudFront Guide](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/) |
| 26/06/2026 | Thứ 6 | - Tối ưu hóa hiệu năng CloudFront: kích hoạt nén dữ liệu tự động gzip và Brotli, điều chỉnh TTL Cache-Control headers.<br>- Liên kết bản ghi Alias Record từ Route 53 trỏ trực tiếp đến domain của CloudFront Distribution.<br>- Đo lường và so sánh độ trễ trước và sau khi có CDN. Tổng kết tuần 5. | Tối ưu hiệu năng CDN với Caching Behaviors và Route 53 Alias | [CloudFront Optimization](https://aws.amazon.com/caching/cdn/) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Nắm vững kỹ thuật Multi-stage Docker build: tách biệt môi trường build chứa compiler nặng khỏi môi trường runtime chỉ chứa file chạy tối thiểu, giảm dung lượng image từ 800MB xuống còn 45MB.
  - Hiểu rõ cơ chế xác thực ngắn hạn của Docker CLI đối với Amazon ECR thông qua token mã hóa từ AWS STS.
  - Nắm vững quy trình phân giải tên miền toàn cầu với Route 53 và lợi ích của bản ghi AWS Alias Record tự động cập nhật IP của tài nguyên AWS.
  - Làm chủ giải pháp bảo vệ dữ liệu với CloudFront Origin Access Control, đảm bảo dữ liệu gốc trên S3 luôn được bảo vệ an toàn.
- Kết quả đạt được:
  - 01 Docker Image tối ưu được lưu trữ và quét bảo mật tự động trên Amazon ECR Private Repository.
  - 01 Hệ thống DNS hoàn chỉnh trên Amazon Route 53 với các bản ghi được ánh xạ chính xác.
  - 01 Amazon CloudFront Distribution phân phối tài nguyên toàn cầu với Origin Access Control bảo mật, giảm độ trễ truy cập hơn 65%.

### Khó khăn và hướng giải quyết:
- Khó khăn: Sau khi triển khai CloudFront Distribution với S3 Bucket, truy cập vào đường link CloudFront bị trả về mã lỗi 403 Forbidden AccessDenied.
- Hướng giải quyết: Phân tích nguyên nhân do đã cấu hình Origin Access Control nhưng chưa cập nhật S3 Bucket Policy tương ứng để cấp quyền s3:GetObject cho CloudFront Service Principal với điều kiện ArnLike khớp với ARN của Distribution. Sau khi cập nhật lại chính sách Bucket Policy, lỗi 403 đã được xử lý thành công.
