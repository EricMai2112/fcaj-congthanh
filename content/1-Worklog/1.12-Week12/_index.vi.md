---
title: "Tuần 12: Hoàn thiện dự án, tổng kết báo cáo và nghiệm thu"
date: 2026-08-10
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Chủ đề:
Hoàn thiện các tính năng dự án, tối ưu hóa mã nguồn, tổng hợp báo cáo thực tập song ngữ và nghiệm thu đánh giá cùng Mentor và đại diện doanh nghiệp

### Mục tiêu tuần:
- Rà soát và hoàn thiện các chức năng mở rộng còn lại ở cả Frontend và Backend; giải quyết triệt để các lỗi phát sinh trong quá trình tích hợp.
- Tối ưu hóa cấu trúc mã nguồn, chuẩn hóa tài liệu kỹ thuật và cấu hình triển khai để hệ thống đạt độ ổn định và dễ bảo trì lâu dài.
- Hoàn thiện toàn bộ nội dung của trang Báo cáo thực tập tốt nghiệp trên Hugo Workshop Template theo định dạng song ngữ Tiếng Việt và Tiếng Anh.
- Tổ chức buổi thuyết trình tổng kết kỳ thực tập, báo cáo kết quả trước Mentor Nguyễn Gia Hưng và hoàn tất thủ tục đánh giá, xin mộc xác nhận từ Công ty TNHH Amazon Web Services Việt Nam.

### Chi tiết công việc theo ngày (10/08/2026 - 14/08/2026):

| Ngày | Thứ | Nội dung công việc | Lab / Dự án thực hành | Nguồn tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| 10/08/2026 | Thứ 2 | - Tiến hành rà soát các tính năng mở rộng: quản lý danh sách thành viên nhóm, phân quyền Admin và Member, tính năng tìm kiếm lịch sử tin nhắn.<br>- Xử lý các lỗi ngoại lệ: ký tự đặc biệt trong tin nhắn, kiểm tra giới hạn dung lượng tải tệp tin tại client và backend.<br>- Tối ưu hóa connection pooling giữa Node.js, Redis và cơ sở dữ liệu. | Dự án Chatpulse: Tối ưu hóa tính năng mở rộng và xử lý ngoại lệ | [Node.js Performance Tips](https://nodejs.org/en/docs/guides/) |
| 11/08/2026 | Thứ 3 | - Chuẩn hóa toàn bộ mã nguồn: loại bỏ các dòng log thừa, bổ sung chú thích code, định dạng code đồng nhất với Prettier và ESLint.<br>- Cập nhật file README.md trên GitHub: hướng dẫn cài đặt môi trường máy cá nhân, giải thích các biến môi trường mẫu .env.example, cấu trúc thư mục và quy trình deploy production.<br>- Kiểm tra lại kịch bản CI/CD bảo đảm mã nguồn build thành công không có cảnh báo. | Dự án Chatpulse: Chuẩn hóa mã nguồn và hoàn thiện tài liệu kỹ thuật GitHub | [Professional README Guide](https://www.makeareadme.com/) |
| 12/08/2026 | Thứ 4 | - Tổng hợp toàn bộ hồ sơ thực tập lên website Hugo FCAJ Workshop Template:<br>+ Trang chủ Thông tin sinh viên và ảnh đại diện.<br>+ Nhật ký công việc chi tiết 12 tuần từ tuần 1 đến tuần 12.<br>+ Đề xuất dự án Chatpulse tại Mục 2 Proposal.<br>+ Danh sách bài viết Blogs kỹ thuật tại Mục 3.<br>+ Minh chứng tham gia các sự kiện chuyên môn tại Mục 4 Events.<br>+ Báo cáo kỹ thuật chi tiết tại Mục 5 Workshop.<br>+ Bảng tự đánh giá kết quả thực tập tại Mục 6 và chia sẻ đóng góp ý kiến tại Mục 7. | Báo cáo Thực tập: Hoàn thiện website Báo cáo Hugo Workshop Template | [Hugo Learn Theme](https://learn.netlify.app/) |
| 13/08/2026 | Thứ 5 | - Thực hiện rà soát và đối chiếu song ngữ toàn diện giữa bản Tiếng Việt và bản Tiếng Anh, bảo đảm đồng bộ nội dung.<br>- Kiểm tra toàn bộ các liên kết, hình ảnh sơ đồ kiến trúc, mã nguồn mẫu và video demo nhúng trên website.<br>- Chạy lệnh hugo --minify để kiểm thử bản build production, bảo đảm không có bất kỳ lỗi cú pháp nào. | Báo cáo Thực tập: Thẩm định chất lượng song ngữ và kiểm thử bản Build Production | [Hugo Documentation](https://gohugo.io/documentation/) |
| 14/08/2026 | Thứ 6 | - Tham gia buổi họp tổng kết và báo cáo kết quả thực tập trước Mentor Nguyễn Gia Hưng và đại diện công ty AWS Việt Nam.<br>- Trình bày slide báo cáo kiến trúc hệ thống Chatpulse, demo các tính năng hoạt động thực tế trên AWS và trả lời câu hỏi phản biện chuyên môn.<br>- Nhận xét, tiếp thu góp ý từ Mentor; hoàn tất phiếu đánh giá thực tập và tiến hành các thủ tục xin xác nhận của công ty. Hoàn thành kỳ thực tập 12 tuần. | Tổng kết Thực tập: Báo cáo nghiệm thu dự án và tiếp nhận đánh giá từ Mentor | [AWS Community Vietnam](https://aws.amazon.com/) |

### Kiến thức và kết quả đạt được:
- Kiến thức:
  - Kỹ năng hoàn thiện và đóng gói sản phẩm phần mềm theo quy trình chuẩn của ngành công nghệ.
  - Làm chủ hệ sinh thái AWS Cloud: từ mạng VPC, Route 53, CloudFront, máy chủ EC2, lưu trữ S3, bộ đệm ElastiCache, bảo mật IAM, WAF, ACM đến giám sát CloudWatch và gửi mail SES.
  - Rèn luyện tư duy phản biện và kỹ năng bảo vệ giải pháp kiến trúc trước các chuyên gia kỹ thuật.
  - Tác phong kỷ luật và văn hóa làm việc chuyên nghiệp tại doanh nghiệp công nghệ.
- Kết quả đạt được:
  - Mã nguồn dự án Chatpulse hoàn chỉnh, tài liệu hướng dẫn chi tiết trên GitHub.
  - Website Báo cáo thực tập FCAJ song ngữ hoàn chỉnh, đạt chuẩn barem điểm của chương trình.
  - Phiếu đánh giá thực tập hoàn tất với xác nhận từ Công ty TNHH Amazon Web Services Việt Nam.

### Khó khăn và hướng giải quyết:
- Khó khăn: Duy trì tính đồng bộ nội dung song ngữ giữa hai phiên bản tiếng Việt và tiếng Anh cho khối lượng tài liệu kỹ thuật lớn trong 12 tuần.
- Hướng giải quyết: Xây dựng checklist kiểm tra theo từng thư mục của Hugo Template, đối chiếu song song cấu trúc file từng tuần, đồng thời sử dụng thuật ngữ kỹ thuật nhất quán trên cả hai ngôn ngữ. Nhờ vậy bài báo cáo đạt được sự chỉn chu và đồng bộ.
