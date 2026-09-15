---
title: "Tuần 1: Định hướng thực tập và thiết lập nền tảng bảo mật"
date: 2026-05-25
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Chủ đề:
Định hướng thực tập, văn hóa AWS và thiết lập nền tảng quản trị bảo mật tài khoản

### Mục tiêu tuần:
- Tìm hiểu quy định, văn hóa làm việc tại Amazon Web Services Việt Nam và quy chế chương trình FCAJ.
- Thiết lập tài khoản AWS cá nhân, cấu hình AWS Budgets và CloudWatch Billing Alerts để kiểm soát chi phí trong suốt quá trình thực tập.
- Thực hành thiết lập bảo mật cấp quản trị với AWS Identity and Access Management (IAM): Users, Groups, Roles, Policies và kích hoạt xác thực đa yếu tố MFA.
- Cài đặt, cấu hình và sử dụng thành thạo AWS CLI trên môi trường máy cá nhân.

### Chi tiết công việc theo ngày (25/05/2026 - 29/05/2026):

| Ngày | Thứ | Nội dung công việc | Lab / Dự án thực hành | Nguồn tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| 25/05/2026 | Thứ 2 | - Tham gia buổi định hướng với đại diện công ty và Mentor Nguyễn Gia Hưng.<br>- Tìm hiểu văn hóa làm việc, quy định bảo mật thông tin và tiêu chuẩn đánh giá kỳ thực tập FCAJ. | Tìm hiểu hệ sinh thái đào tạo FCAJ và bộ quy tắc AWS Well-Architected Framework | [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/) |
| 26/05/2026 | Thứ 3 | - Đăng ký tài khoản AWS cá nhân phục vụ thực hành.<br>- Kích hoạt xác thực đa yếu tố MFA cho tài khoản Root.<br>- Khóa Root user và tạo tài khoản IAM Administrator với quyền hạn kiểm soát. | Cấu hình bảo mật tài khoản Root và khởi tạo IAM Admin User | [AWS IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |
| 27/05/2026 | Thứ 4 | - Tìm hiểu cơ chế tính phí đám mây và chính sách AWS Free Tier.<br>- Cấu hình AWS Budgets với ngân sách dự kiến 5 USD một tháng.<br>- Tạo CloudWatch Billing Alarm gửi email thông báo qua Amazon SNS khi chi phí vượt 80% ngân sách. | Quản lý chi phí với AWS Budgets và thiết lập Billing Alarm | [AWS Cost Management](https://aws.amazon.com/aws-cost-management/) |
| 28/05/2026 | Thứ 5 | - Cài đặt AWS CLI v2 trên máy tính cá nhân.<br>- Tạo IAM Access Key và Secret Key cho developer user và thực hiện cấu hình qua lệnh aws configure.<br>- Kiểm tra cấu hình kết nối qua các lệnh: aws sts get-caller-identity, aws ec2 describe-regions. | Cài đặt AWS CLI, xác thực và các thao tác cơ bản | [AWS CLI User Guide](https://docs.aws.amazon.com/cli/latest/userguide/) |
| 29/05/2026 | Thứ 6 | - Thực hành phân quyền IAM: tạo Groups cho Developers và CloudAdmins, gán Managed Policies.<br>- Viết IAM Custom Policy dạng JSON theo nguyên tắc quyền tối thiểu, chỉ cho phép đọc dữ liệu EC2 và S3.<br>- Tổng hợp báo cáo tuần 1 và họp review tiến độ với Mentor. | Cấu hình nâng cao IAM Groups, Custom Policies và phân quyền tối thiểu | [IAM JSON Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Hiểu rõ mô hình chia sẻ trách nhiệm bảo mật của AWS.
  - Nắm vững nguyên tắc quyền tối thiểu trong quản trị danh tính IAM.
  - Hiểu cách hoạt động của AWS CLI, cấu trúc câu lệnh và xác thực an toàn qua Access Keys.
- Kết quả đạt được:
  - 01 Tài khoản AWS cá nhân được thiết lập bảo mật với MFA cho tài khoản Root và sử dụng IAM User cho công việc hàng ngày.
  - 01 AWS Budget và CloudWatch Billing Alarm hoạt động ổn định, sẵn sàng cảnh báo chi phí phát sinh.
  - Môi trường máy tính cá nhân được cấu hình hoàn chỉnh với AWS CLI v2.

### Khó khăn và hướng giải quyết:
- Khó khăn:
  - Khi đăng ký tài khoản AWS cá nhân mới, quá trình xác thực số điện thoại và thẻ thanh toán quốc tế gặp sự cố phản hồi từ cổng viễn thông, dẫn đến trạng thái tài khoản bị tạm giữ để xác minh bổ sung và chưa thể kích hoạt đầy đủ dịch vụ ngay.
  - Khi cấu hình Billing Alarm trên CloudWatch, số liệu chi phí ban đầu không hiển thị ngay do hệ thống tính toán hóa đơn cập nhật theo chu kỳ định kỳ.
- Hướng giải quyết:
  - Chủ động liên hệ và mở case làm việc trực tiếp với đội ngũ **AWS Support**, trao đổi và cung cấp thông tin xác thực danh tính cá nhân phục vụ chương trình thực tập sinh **FCAJ**, qua đó được phía AWS hỗ trợ kiểm tra thủ công, phê duyệt nhanh chóng và kích hoạt hoàn tất tài khoản trong thời gian ngắn.
  - Tra cứu tài liệu từ AWS Support, kích hoạt tùy chọn Receive Billing Alerts trong phần cài đặt Preferences của tài khoản Root, sau đó thực hiện kiểm tra luồng thông báo của SNS để bảo đảm email cảnh báo hoạt động chính xác.
