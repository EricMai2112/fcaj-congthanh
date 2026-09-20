---
title: "Tuần 4: Serverless, hạ tầng dạng mã nguồn và Well-Architected"
date: 2026-06-15
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Chủ đề:
Nghiên cứu kiến trúc Serverless với AWS Lambda và API Gateway, tự động hóa hạ tầng với Infrastructure as Code và khung kiến trúc AWS Well-Architected

### Mục tiêu tuần:
- Làm chủ mô hình điện toán không máy chủ: xây dựng hàm xử lý sự kiện với AWS Lambda và tích hợp qua REST API trên Amazon API Gateway.
- Tiếp cận phương pháp quản lý hạ tầng dưới dạng mã nguồn thông qua AWS CloudFormation và AWS CDK.
- Nghiên cứu 5 trụ cột của AWS Well-Architected Framework và áp dụng phương pháp luận tối ưu hóa chi phí vào thiết kế hệ thống.

### Chi tiết công việc theo ngày (15/06/2026 - 19/06/2026):

| Ngày       | Thứ   | Nội dung công việc                                                                                                                                                                                                                                                                      | Lab / Dự án thực hành                                                                                                                                                                     |
| :--------- | :---- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 15/06/2026 | Thứ 2 | - Tìm hiểu kiến trúc Serverless: mô hình hướng sự kiện, mô hình chi phí theo lượng dùng và cơ chế khởi động lạnh.<br>- Tạo hàm AWS Lambda đầu tiên bằng Node.js runtime xử lý tính toán số học.<br>- Cấu hình IAM Execution Role cho Lambda với quyền ghi nhật ký vào Amazon CloudWatch Logs. | [000022 - Tự động hóa bằng Serverless với AWS Lambda](https://000022.awsstudygroup.com/vi/)                                                                                               |
| 16/06/2026 | Thứ 3 | - Khởi tạo REST API trên Amazon API Gateway.<br>- Tạo Resource /calculate và Method POST, cấu hình Lambda Proxy Integration để chuyển tiếp dữ liệu yêu cầu.<br>- Thiết lập CORS và kiểm tra API endpoint qua Postman và curl.                                                              | [000066 - Xây dựng API Serverless với API Gateway](https://000066.awsstudygroup.com/vi/)                                                                                                 |
| 17/06/2026 | Thứ 4 | - Nghiên cứu nguyên lý Infrastructure as Code và cú pháp YAML của AWS CloudFormation.<br>- Viết CloudFormation Template khởi tạo hạ tầng cơ bản gồm S3 Bucket và IAM Role.<br>- Thực hành triển khai stack qua giao diện CloudFormation Console và kiểm tra trạng thái hoàn thành.         | [000037 - Hạ tầng dưới dạng mã với AWS CloudFormation](https://000037.awsstudygroup.com/vi/)                                                                                             |
| 18/06/2026 | Thứ 5 | - Mở rộng template CloudFormation: thêm tham số Parameters, điều kiện Conditions và giá trị đầu ra Outputs.<br>- Thử nghiệm cơ chế Rollback tự động khi gặp lỗi cấu hình tài nguyên.<br>- Tìm hiểu cơ bản về AWS Cloud Development Kit sử dụng TypeScript để định nghĩa tài nguyên đám mây. | - [000037 - CloudFormation với Parameters và Rollback](https://000037.awsstudygroup.com/vi/)<br>- [000038 - Bộ công cụ phát triển đám mây AWS CDK](https://000038.awsstudygroup.com/vi/) |
| 19/06/2026 | Thứ 6 | - Nghiên cứu 5 trụ cột của AWS Well-Architected Framework: Vận hành xuất sắc, Bảo mật, Độ tin cậy, Hiệu quả hiệu năng, Tối ưu chi phí.<br>- Sử dụng công cụ AWS Well-Architected Tool để tự đánh giá hệ thống thực hành đã xây dựng.<br>- Lập danh sách các khuyến nghị tối ưu chi phí. Tổng kết tuần 4. | - [000042 - Tối ưu chi phí với Savings Plans](https://000042.awsstudygroup.com/vi/)<br>- [Đánh giá kiến trúc với AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Hiểu rõ cơ chế hoạt động hướng sự kiện của Lambda, vòng đời thực thi và cách tối ưu thời gian khởi động.
  - Nắm vững vai trò của API Gateway trong việc làm cửa ngõ định tuyến, xác thực, điều tiết lưu lượng và quản lý phiên.
  - Thấu hiểu lợi ích của Infrastructure as Code: hạ tầng có thể tái lập, quản lý phiên bản qua Git và loại bỏ sai sót cấu hình thủ công.
  - Nắm vững các tiêu chí cốt lõi của AWS Well-Architected Framework làm kim chỉ nam thiết kế cho dự án thực tập.
- Kết quả đạt được:
  - 01 Dịch vụ API Serverless hoàn chỉnh gồm API Gateway, Lambda và CloudWatch Logs phản hồi nhanh dưới 100ms.
  - 01 CloudFormation Template mẫu có thể tái sử dụng để sinh hạ tầng tự động.
  - Bảng đánh giá Well-Architected Review sơ bộ cho các dịch vụ đang vận hành.

### Khó khăn và hướng giải quyết:
- Khó khăn: Khi gửi yêu cầu từ ứng dụng frontend cục bộ đến API Gateway thì gặp lỗi CORS do thiếu header Access-Control-Allow-Origin.
- Hướng giải quyết: Tìm hiểu cơ chế bảo mật CORS của trình duyệt. Nhận thấy khi sử dụng Lambda Proxy Integration, ngoài việc bật CORS trên giao diện API Gateway Console cho phương thức OPTIONS, hàm Lambda cần trả về đầy đủ các header Access-Control-Allow-Origin và Access-Control-Allow-Methods trong kết quả phản hồi. Sau khi bổ sung các header này, lỗi CORS đã được xử lý.
