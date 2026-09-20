---
title: "Blog 5: Bứt Phá Xử Lý Tài Liệu Doanh Nghiệp Với GenAI IDP Accelerator"
menuTitle: "Blog 5"
date: 2026-08-12
weight: 5
chapter: false
pre: " <b> 3.5. </b> "
---

**Ngày đăng:** 12/08/2026  
**Link bài viết:** [https://www.facebook.com/groups/awsstudygroupfcj/permalink/2241356219962671/](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2241356219962671/)  

---

Xin chào mọi người, trong kỷ nguyên chuyển đổi số, Xử lý tài liệu thông minh (Intelligent Document Processing - IDP) luôn là một trong những bài toán mất rất nhiều thời gian và chi phí nhất của doanh nghiệp. Ước tính có tới 80–90% dữ liệu nằm ở dạng không cấu trúc trong các tệp PDF, hợp đồng, hóa đơn hay hồ sơ y tế. Các giải pháp OCR hay ML truyền thống dựa trên mẫu (template) thường rất dễ vỡ khi định dạng tài liệu thay đổi.

Hôm nay, tôi muốn chia sẻ với mọi người những góc nhìn và phân tích của mình sau khi tìm hiểu một bài viết giải pháp mã nguồn mở cực kỳ giá trị từ đội ngũ chuyên gia AWS: **GenAI IDP Accelerator** – bộ công cụ giúp rút ngắn thời gian triển khai quy trình xử lý tài liệu bằng Generative AI từ vài tháng xuống chỉ còn vài ngày.

![Kiến trúc tổng quan hệ thống GenAI IDP Accelerator trên AWS](/images/3-BlogsPosted/blog5-genai-idp-accelerator.png?featherlight=false&width=100%)

---

### 1. ĐIỂM NỔI BẬT VÀ LỢI ÍCH CỦA GENAI IDP ACCELERATOR

Điểm đắt giá nhất của giải pháp **GenAI IDP Accelerator** là nó giải quyết đúng điểm nghẽn từ giai đoạn thử nghiệm đến Production. Rất nhiều doanh nghiệp làm demo chạy rất tốt với vài ba tài liệu, nhưng khi đưa vào vận hành với hàng ngàn bản ghi mỗi ngày thì hệ thống bị nghẽn, chi phí tăng vọt hoặc sai sót dữ liệu.

- **Kiến trúc xử lý hợp nhất 2 chế độ:** Chuyển đổi linh hoạt ngay trong lúc runtime mà không cần redeploy:
  - *Chế độ BDA (Amazon Bedrock Data Automation):* Dịch vụ được AWS quản lý hoàn toàn, tính phí đơn giản theo số trang, phù hợp cho đa số các bài toán chuẩn.
  - *Chế độ Bedrock Pipeline:* Kết hợp Amazon Textract với các mô hình Bedrock (Nova, Claude 3.5 Sonnet...) dành cho các tài liệu cực kỳ phức tạp cần custom logic riêng.
- **Tích hợp Review con người (Human-in-the-loop):** Giao diện Web tích hợp sẵn luồng duyệt dữ liệu cho các trường hợp điểm tin cậy thấp.
- **Test Studio & AI Agent Companion:** Cho phép so sánh benchmark độ chính xác/chi phí giữa các mode, đồng thời tích hợp AI Agent cho phép truy vấn analytics bằng câu lệnh tự nhiên.
- **Khả năng tách & Phân loại tài liệu thông minh:** Tự động nhận diện và chia nhỏ một tệp PDF gồm nhiều tài liệu hỗn hợp (ví dụ: hồ sơ vay vốn chứa cả căn cước, sao kê, hợp đồng).

---

### 2. HIỆU QUẢ THỰC TẾ ĐÃ ĐƯỢC CHỨNG MINH

Trong bài viết, AWS đã chia sẻ hai câu chuyện thực tế chứng minh sức mạnh của bộ công cụ này:

- **Competiscan (Công ty nghiên cứu thị trường):**
  - *Thách thức:* Xử lý 35,000 – 45,000 chiến dịch marketing mỗi ngày trên kho lưu trữ 45 triệu chiến dịch.
  - *Kết quả:* Đạt 85% độ chính xác trong bóc tách và phân loại; đưa hệ thống vào Production chỉ trong 8 tuần.
- **Ricoh (Tập đoàn quản lý tài liệu toàn cầu):**
  - *Thách thức:* Phân loại và bóc tách hồ sơ y tế với khối lượng từ 10,000 đến 70,000 tài liệu/tháng.
  - *Kết quả:* Tiết kiệm hơn 1,900 giờ làm việc mỗi năm, giảm thiểu tối đa các lỗi phạt tài chính nhờ bóc tách chuẩn xác.

---

### 3. KIẾN TRÚC TỔNG QUAN HỆ THỐNG

Bộ giải pháp được xây dựng hoàn toàn trên hạ tầng Serverless của AWS (**AWS Lambda**, **AWS Step Functions**, **Amazon S3**, **Amazon Bedrock**, **Amazon SQS**, **Amazon DynamoDB**, **AWS AppSync**), đảm bảo khả năng tự động co giãn theo lưu lượng và chỉ tính phí khi có tài liệu được xử lý.

---

### 4. CẢM NGHĨ VÀ GÓC NHÌN CÁ NHÂN

- Điều tôi thích nhất ở giải pháp này là bạn không cần sửa code core khi cần định nghĩa một loại tài liệu mới. Tất cả việc thêm field cần bóc tách, chỉnh sửa prompt hay quy tắc validation đều được quản lý bằng file cấu hình JSON/YAML hoặc thao tác trực tiếp trên giao diện Web UI.
- Sự linh hoạt giữa hai chế độ BDA và Bedrock Pipeline giúp doanh nghiệp tối ưu hóa bài toán chi phí: Với các tài liệu chuẩn (Hóa đơn, ID, Chứng từ), BDA cung cấp mức giá cố định theo trang rất rẻ. Với các tài liệu dị biệt, pipeline tùy biến với Bedrock sẽ giúp giải quyết triệt để các ca khó.

---

### 5. TÀI LIỆU THAM KHẢO

- [AWS Machine Learning Blog - Accelerate intelligent document processing with Generative AI on AWS](https://aws.amazon.com/blogs/machine-learning/accelerate-intelligent-document-processing-with-generative-ai-on-aws/)
