---
title: "Tuần 2: Hạ tầng mạng VPC, máy chủ EC2 và lưu trữ tĩnh S3"
date: 2026-06-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Chủ đề:
Thiết kế và triển khai mạng ảo Amazon VPC, máy chủ tính toán Amazon EC2 và lưu trữ tĩnh Amazon S3

### Mục tiêu tuần:
- Nắm vững kiến trúc mạng ảo trên đám mây: thiết kế Custom VPC với Public Subnets, Private Subnets, Internet Gateway, NAT Gateway và định tuyến qua Route Tables.
- Triển khai máy chủ tính toán Amazon EC2, cấu hình cơ chế bảo mật mạng đa lớp với Security Groups và Network ACLs.
- Cấu hình web server Nginx trên EC2, thiết lập kết nối SSH qua Key Pair an toàn.
- Khởi tạo Amazon S3 Bucket, thực hành lưu trữ đối tượng, cấu hình Bucket Versioning và tính năng Static Website Hosting.

### Chi tiết công việc theo ngày (01/06/2026 - 05/06/2026):

| Ngày       | Thứ   | Nội dung công việc                                                                                                                                                                                                                  | Lab / Dự án thực hành                                                                                                                                                                    |
| :--------- | :---- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 01/06/2026 | Thứ 2 | - Tìm hiểu lý thuyết VPC: dải IP, CIDR blocks và chia subnet.<br>- Khởi tạo Custom VPC dải 10.0.0.0/16 tại Region Singapore ap-southeast-1.<br>- Tạo 02 Public Subnets và 02 Private Subnets trải dài trên 2 Availability Zones ap-southeast-1a và ap-southeast-1b. | [000003 - Khởi tạo Custom VPC và Subnets](https://000003.awsstudygroup.com/vi/)                                                                                                        |
| 02/06/2026 | Thứ 3 | - Khởi tạo Internet Gateway và gắn vào Custom VPC.<br>- Cấu hình Public Route Table định tuyến 0.0.0.0/0 ra Internet Gateway và liên kết với các Public Subnets.<br>- Khởi tạo NAT Gateway đặt tại Public Subnet và cấu hình Private Route Table định tuyến lưu lượng ra Internet cho Private Subnet. | [000003 - Cấu hình Internet Gateway, NAT Gateway và Route Tables](https://000003.awsstudygroup.com/vi/)                                                                                 |
| 03/06/2026 | Thứ 4 | - Khởi tạo máy chủ Amazon EC2 Ubuntu 22.04 LTS instance type t3.micro trong Public Subnet.<br>- Tạo mới EC2 Key Pair lưu trữ an toàn trên máy cá nhân.<br>- Cấu hình Security Group: cho phép cổng 22 SSH cho IP cá nhân và cổng 80 HTTP cho toàn bộ dải mạng. | [000004 - Khởi tạo và bảo mật máy chủ Amazon EC2](https://000004.awsstudygroup.com/vi/)                                                                                                 |
| 04/06/2026 | Thứ 5 | - Thực hiện kết nối SSH an toàn vào máy chủ EC2 thông qua terminal.<br>- Cập nhật hệ thống, cài đặt và cấu hình Nginx Web Server chạy trang giới thiệu cơ bản.<br>- Nghiên cứu Network ACLs: phân tích sự khác nhau giữa Security Group và Network ACL, cấu hình quy tắc kiểm soát lưu lượng tầng subnet. | - [000004 - Kết nối và cấu hình Web Server trên EC2](https://000004.awsstudygroup.com/vi/)<br>- [000003 - Tường lửa và Network ACLs trong VPC](https://000003.awsstudygroup.com/vi/) |
| 05/06/2026 | Thứ 6 | - Nghiên cứu Amazon S3: quy tắc đặt tên bucket, các lớp lưu trữ storage classes.<br>- Tạo S3 Bucket, kích hoạt Bucket Versioning để chống ghi đè và xóa nhầm dữ liệu.<br>- Cấu hình S3 Static Website Hosting, viết S3 Bucket Policy cho phép đọc trang web và kiểm tra truy cập qua S3 Website Endpoint. Tổng kết tuần 2. | [000057 - Hosting Website tĩnh với Amazon S3](https://000057.awsstudygroup.com/vi/)                                                                                                    |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Nắm vững cách phân chia dải mạng CIDR và kiến trúc phân tầng mạng giữa Public Subnet cho dịch vụ hướng ra ngoài và Private Subnet cho Database và Backend.
  - Hiểu rõ vai trò của NAT Gateway trong việc cho phép máy chủ trong Private Subnet tải bản cập nhật ra ngoài nhưng chặn truy cập từ Internet vào trong.
  - Phân biệt rõ ràng giữa Security Group ở cấp máy chủ và Network ACL ở cấp subnet.
  - Làm chủ kỹ thuật lưu trữ đối tượng và hosting web tĩnh chi phí thấp trên Amazon S3.
- Kết quả đạt được:
  - 01 Hệ thống mạng Custom VPC đa vùng khả dụng hoàn chỉnh với Internet Gateway, NAT Gateway và 2 bảng định tuyến Route Tables.
  - 01 Máy chủ EC2 chạy Nginx phục vụ website tĩnh thử nghiệm, truy cập thành công qua Public IP.
  - 01 S3 Bucket được cấu hình Static Hosting và bật bảo vệ dữ liệu với Versioning.

### Khó khăn và hướng giải quyết:
- Khó khăn: Ban đầu không thể kết nối SSH vào EC2 instance khi vừa khởi tạo xong, terminal báo lỗi timeout kết nối.
- Hướng giải quyết: Thực hiện kiểm tra định tuyến mạng: kiểm tra cấp phát Public IP, kiểm tra bảng định tuyến của Public Subnet đã trỏ 0.0.0.0/0 về Internet Gateway chưa, kiểm tra Security Group đã mở cổng 22 chưa. Sau khi phát hiện quên gán Route Table vào Public Subnet và cập nhật lại, kết nối SSH đã thành công.
