---
title: "Dọn dẹp tài nguyên"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### Quy Trình Dọn Dẹp Theo Thứ Tự Khuyến Nghị

Để tránh lỗi ràng buộc phụ thuộc khi xóa tài nguyên trên AWS, thực hiện theo đúng trình tự sau:

#### 1. Dọn dẹp Máy chủ Amazon EC2
1. Mở dịch vụ **Amazon EC2**, chọn mục **Instances**.
2. Chọn máy chủ `ChatPulse-Backend-Server`, chọn **Instance state**, chọn **Terminate instance** và xác nhận xóa.
3. Kiểm tra mục **Elastic IPs**, chọn địa chỉ IP tĩnh `54.254.6.80`, chọn **Actions**, chọn **Release Elastic IP addresses** để giải phóng IP và tránh bị tính phí IP nhàn rỗi.

#### 2. Xóa cụm Amazon ElastiCache Redis
1. Mở dịch vụ **Amazon ElastiCache**, chọn mục **Redis OSS caches**.
2. Chọn cụm cache Redis của ChatPulse và nhấn **Delete**.
3. Chọn tùy chọn *No* tại mục Create final backup để tiến hành xóa ngay lập tức.

#### 3. Vô hiệu hóa và Xóa Amazon CloudFront Distribution
1. Mở dịch vụ **CloudFront**, chọn phân phối gắn với tên miền `ericmai.io.vn`.
2. Nhấn nút **Disable**, chờ khoảng 3 đến 5 phút để mạng phân phối trên toàn cầu chuyển sang trạng thái Disabled.
3. Sau khi đã Disabled, chọn lại phân phối và nhấn **Delete**.

#### 4. Dọn dẹp tệp tin và xóa Amazon S3 Bucket
1. Mở dịch vụ **Amazon S3**, chọn bucket chứa mã nguồn tĩnh Frontend.
2. Nhấn nút **Empty**, nhập dòng chữ `permanently delete` để xóa sạch toàn bộ mã nguồn build và ảnh đã lưu.
3. Sau khi bucket đã trống, nhấn nút **Delete** để xóa hoàn toàn bucket khỏi tài khoản.

#### 5. Xóa luồng CI/CD với AWS CodePipeline và AWS CodeBuild
1. Mở **AWS CodePipeline**, chọn pipeline của dự án và nhấn **Delete pipeline**.
2. Mở **AWS CodeBuild**, chọn Build projects và chọn **Delete build project**.
3. Truy cập **IAM Console** để xóa các Service Role phụ trợ do CodeBuild và CodePipeline tự động tạo nếu không còn nhu cầu sử dụng.

#### 6. Xóa Web ACL trên AWS WAF
1. Mở **AWS WAF & Shield**, chuyển Region sang **Global CloudFront**.
2. Kiểm tra tab *Associated AWS resources*, đảm bảo không còn tài nguyên CloudFront nào đang liên kết.
3. Chọn Web ACL của ChatPulse và nhấn **Delete**.

#### 7. Dọn dẹp bản ghi Amazon Route 53
1. Mở **Amazon Route 53**, chọn Hosted Zone `ericmai.io.vn`.
2. Xóa các bản ghi loại A trỏ Alias CloudFront hoặc EC2, xóa các bản ghi CNAME xác thực ACM và SES không còn sử dụng, giữ lại hai bản ghi mặc định NS và SOA.

#### 8. Dọn dẹp Security Groups và Cảnh báo CloudWatch
1. Mở **VPC Console**, chọn **Security Groups**, xóa các nhóm bảo mật đã tạo cho dự án gồm Security Group của EC2 Backend và Security Group của ElastiCache Redis.
2. Mở **Amazon CloudWatch**, chọn mục **Alarms**, chọn cảnh báo ngưỡng CPU đã thiết lập cho máy chủ và nhấn **Delete** để hoàn tất quá trình dọn dẹp.
