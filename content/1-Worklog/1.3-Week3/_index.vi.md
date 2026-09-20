---
title: "Tuần 3: Cơ sở dữ liệu RDS, DynamoDB và giám sát CloudWatch"
date: 2026-06-08
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Chủ đề:
Triển khai cơ sở dữ liệu đám mây Amazon RDS, Amazon DynamoDB và giám sát vận hành hệ thống với Amazon CloudWatch

### Mục tiêu tuần:
- Triển khai cơ sở dữ liệu quan hệ Amazon RDS PostgreSQL trong Private Subnet theo kiến trúc đa vùng khả dụng.
- Thực hành với cơ sở dữ liệu NoSQL Amazon DynamoDB, thiết kế bảng dữ liệu tối ưu và cấu hình sao lưu Point-in-Time Recovery.
- Cài đặt và cấu hình CloudWatch Unified Agent trên máy chủ EC2 để thu thập chỉ số bộ nhớ RAM và nhật ký ứng dụng.
- Xây dựng CloudWatch Dashboard trực quan hóa hiệu năng và thiết lập CloudWatch Alarms gửi email cảnh báo qua Amazon SNS.

### Chi tiết công việc theo ngày (08/06/2026 - 12/06/2026):

| Ngày       | Thứ   | Nội dung công việc                                                                                                                                                                                                                                                              | Lab / Dự án thực hành                                                                       |
| :--------- | :---- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------ |
| 08/06/2026 | Thứ 2 | - Tìm hiểu dịch vụ Amazon RDS.<br>- Tạo DB Subnet Group gồm 2 Private Subnets nằm trên 2 Availability Zones khác nhau.<br>- Khởi tạo cơ sở dữ liệu Amazon RDS PostgreSQL instance class db.t3.micro, cấu hình Storage Auto-scaling và tính năng sao lưu tự động.                 | [000005 - Khởi tạo Amazon RDS PostgreSQL](https://000005.awsstudygroup.com/vi/)            |
| 09/06/2026 | Thứ 3 | - Thiết lập Security Group cho RDS: chỉ cho phép cổng 5432 bắt nguồn từ Security Group của máy chủ EC2 App Server.<br>- Cài đặt postgresql-client trên EC2 và thực hiện kết nối thử nghiệm đến RDS qua Private Endpoint.<br>- Tạo bảng mẫu, thực hiện thao tác kiểm tra thêm, đọc dữ liệu. | [000005 - Kết nối và bảo mật Amazon RDS](https://000005.awsstudygroup.com/vi/)              |
| 10/06/2026 | Thứ 4 | - Nghiên cứu cơ chế hoạt động của NoSQL Amazon DynamoDB.<br>- Khởi tạo DynamoDB Table với Partition Key là userId và Sort Key là timestamp.<br>- Thao tác dữ liệu qua AWS CLI và Console, cấu hình Time-to-Live tự động hủy bản ghi cũ và kích hoạt Point-in-time Recovery.     | [000060 - Làm việc với Amazon DynamoDB](https://000060.awsstudygroup.com/vi/)               |
| 11/06/2026 | Thứ 5 | - Cài đặt CloudWatch Unified Agent trên máy chủ Linux EC2.<br>- Gán IAM Role với chính sách CloudWatchAgentServerPolicy cho instance.<br>- Cấu hình file config.json của CloudWatch Agent để thu thập chỉ số bộ nhớ RAM và đẩy nhật ký Nginx về CloudWatch Logs.               | [000008 - Giám sát chỉ số và Logs với CloudWatch](https://000008.awsstudygroup.com/vi/)     |
| 12/06/2026 | Thứ 6 | - Thiết kế CloudWatch Dashboard tập trung theo dõi đồng thời CPU EC2, dung lượng RAM, Disk IOPS và số lượng kết nối Database của RDS.<br>- Cấu hình 02 CloudWatch Alarms: cảnh báo khi CPU EC2 vượt ngưỡng 80% và cảnh báo khi dung lượng trống của RDS dưới 1GB.<br>- Tích hợp Amazon SNS Topic gửi email khẩn cấp đến hộp thư cá nhân khi trạng thái chuyển sang báo động. Tổng kết tuần 3. | [000008 - Thiết lập CloudWatch Dashboards và Alarms](https://000008.awsstudygroup.com/vi/)  |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Hiểu rõ kiến trúc bảo vệ cơ sở dữ liệu trên đám mây: không gán Public IP cho Database, cô lập trong Private Subnet và kiểm soát truy cập bằng cách tham chiếu Security Group ID của máy chủ ứng dụng.
  - Phân biệt sự khác nhau giữa cơ sở dữ liệu quan hệ RDS và cơ sở dữ liệu NoSQL DynamoDB.
  - Phân biệt giữa các chỉ số phần cứng tầng ảo hóa và các chỉ số hệ điều hành cần agent thu thập như RAM và Disk.
- Kết quả đạt được:
  - 01 Database RDS PostgreSQL hoạt động an toàn trong Private Subnet, kết nối thành công từ EC2.
  - 01 DynamoDB Table với tính năng tự động dọn dữ liệu TTL và bảo vệ dữ liệu Point-in-time Recovery.
  - 01 CloudWatch Dashboard hiển thị biểu đồ tài nguyên và 02 Alarms kích hoạt gửi email thông báo qua SNS.

### Khó khăn và hướng giải quyết:
- Khó khăn: Không tìm thấy chỉ số sử dụng bộ nhớ RAM của EC2 trên giao diện CloudWatch mặc định.
- Hướng giải quyết: Tìm hiểu cơ chế giám sát của AWS, nhận biết rằng tầng ảo hóa hypervisor không can thiệp đọc dữ liệu bộ nhớ trong hệ điều hành của khách hàng để bảo đảm tính riêng tư. Cài đặt CloudWatch Unified Agent và phân quyền IAM Role để máy chủ chủ động đẩy chỉ số RAM lên CloudWatch.
