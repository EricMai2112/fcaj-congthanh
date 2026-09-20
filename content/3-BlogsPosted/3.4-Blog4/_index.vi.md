---
title: "Blog 4: Xây Dựng Hệ Thống SRE Multi-Agent Với Amazon Bedrock AgentCore Và MCP"
menuTitle: "Blog 4"
date: 2026-08-04
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

**Ngày đăng:** 04/08/2026  
**Link bài viết:** [https://www.facebook.com/groups/awsstudygroupfcj/permalink/2233932754038351/](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2233932754038351/)  

---

Trong kiến trúc hệ thống hiện đại, công việc của một Kỹ sư Đảm bảo Độ tin cậy Hệ thống (Site Reliability Engineer - SRE) ngày càng trở nên khốc liệt. Khi xảy ra sự cố production, SRE phải xoay xở giữa hàng loạt công cụ: đọc log, xem metric, kiểm tra sự kiện Kubernetes và lật lại các cuốn quy trình vận hành (runbooks) để tìm nguyên nhân gốc rễ. Sự rời rạc này khiến thời gian xử lý sự cố bị kéo dài đáng kể.

Hôm nay, tôi muốn chia sẻ với mọi người những phân tích và cảm nhận của mình sau khi đọc một bài viết chuyên sâu rất hay từ các chuyên gia AWS. Bài viết hướng dẫn cách xây dựng một Trợ lý SRE Đa Đại lý (Multi-Agent SRE Assistant) nâng cao, tận dụng nền tảng **Amazon Bedrock AgentCore**, **LangGraph** và giao thức **Model Context Protocol (MCP)**.

![Kiến trúc hệ thống SRE Multi-Agent với Amazon Bedrock AgentCore và MCP](/images/3-BlogsPosted/blog4-bedrock-agentcore-sre.png?featherlight=false&width=100%)

---

### 1. ĐIỂM NỔI BẬT VÀ LỢI ÍCH

Điểm đắt giá nhất của giải pháp này là khả năng biến các truy vấn kỹ thuật phức tạp thành các câu hội thoại bằng ngôn ngữ tự nhiên. Bạn chỉ cần hỏi: *"Tại sao các pod của payment-service lại bị crash liên tục?"*, hệ thống sẽ tự động tổng hợp dữ liệu từ nhiều nguồn để trả về câu trả lời toàn diện nhất.

- **Supervisor Agent:** Tiếp nhận câu hỏi, lập kế hoạch điều tra, phân công nhiệm vụ cho các đại lý con và tổng hợp báo cáo cuối cùng.
- **Kubernetes Infrastructure Agent:** Chuyên điều tra các vấn đề về pod, deployment, nghẽn tài nguyên và sự kiện trong cụm K8s.
- **Application Logs Agent:** Phân tích log, tìm kiếm các mẫu bất thường xuyên suốt các microservices.
- **Performance Metrics Agent:** Theo dõi thời gian thực và xu hướng lịch sử của các chỉ số hiệu năng.
- **Operational Runbooks Agent:** Tra cứu các tài liệu hướng dẫn và quy trình xử lý sự cố chuẩn của doanh nghiệp.

---

### 2. NHỮNG TÍNH NĂNG CỦA AMAZON BEDROCK AGENTCORE

Qua phân tích bài viết của AWS, tôi nhận thấy bộ công cụ **Amazon Bedrock AgentCore** cung cấp những nền tảng cực kỳ mạnh mẽ để đưa hệ thống AI vào vận hành thực tế:

- **AgentCore Gateway:** Chuyển đổi các API hạ tầng hiện có (K8s, Logs, Metrics) thành các công cụ chuẩn MCP (Model Context Protocol). Điều này cho phép các framework AI mã nguồn mở như LangGraph hay Strands kết nối trực tiếp đến hạ tầng mà không cần viết lại API.
- **AgentCore Memory:** Hệ thống không chỉ lưu lịch sử sự cố mà còn ghi nhớ chân dung người dùng, ngữ cảnh và các phiên tương tác trước đó.
- **AgentCore Runtime:** Cho phép đóng gói Agent thành container ARM64 và deploy lên môi trường Serverless của AWS. Tự động co giãn từ 0 đến hàng ngàn phiên làm việc đồng thời, cách ly tuyệt đối bằng microVM.
- **AgentCore Observability:** Tích hợp sẵn OpenTelemetry để đẩy các chỉ số (LLM metrics, thời gian chạy công cụ MCP, traces) về Amazon CloudWatch giúp giám sát minh bạch toàn bộ quá trình AI suy luận.

---

### 3. KỊCH BẢN ĐIỀU TRA SỰ CỐ THỰC TẾ

Bài viết của AWS đưa ra một kịch bản điều tra rất sát với thực tế vận hành:

- **3.1. Cảnh báo:** Thời gian phản hồi API bị chậm gấp 3 lần trong 1 giờ qua.
- **3.2. Lập kế hoạch:** Supervisor Agent tự động tạo kế hoạch 3 bước: Gọi Metrics Agent kiểm tra độ trễ => Gọi Logs Agent soi lỗi CSDL => Gọi K8s Agent kiểm tra trạng thái Pod.
- **3.3. Phát hiện nguyên nhân gốc rễ (Root Cause):**
  - K8s Agent phát hiện Pod CSDL bị rơi vào trạng thái CrashLoopBackOff do thiếu ConfigMap tên là `database-config`.
  - Logs Agent phát hiện lỗi OutOfMemoryErrors ở service người dùng.
  - Metrics Agent ghi nhận CPU chạm mức 95% và tỷ lệ lỗi lên tới 75%.
- **3.4. Đưa ra giải pháp khắc phục:** Hệ thống không chỉ báo lỗi mà còn đưa ra danh sách các câu lệnh `kubectl` chính xác từng bước để SRE chỉ việc copy-paste và xử lý ngay lập tức.

---

### 4. CẢM NGHĨ VÀ GÓC NHÌN CÁ NHÂN

- Việc phải chuyển đổi ngữ cảnh giữa hàng chục dashboard monitoring trong lúc sự cố xảy ra là nguyên nhân chính gây kiệt sức cho SRE. Việc AI tự động thu thập và xâu chuỗi dữ liệu giúp giảm thời gian điều tra ban đầu từ 30-45 phút xuống chỉ còn 5-10 phút.
- Sự kết hợp giữa AgentCore Gateway và giao thức MCP là một bước đi rất thông minh của AWS. Bạn có thể dùng LangGraph, CrewAI hay bất kỳ framework nào, miễn là hỗ trợ MCP, đều có thể cắm vào hạ tầng AWS một cách an toàn.
- Do hệ thống được triển khai trong môi trường Amazon Bedrock AgentCore Runtime riêng biệt, tích hợp xác thực IAM và Cognito, toàn bộ dữ liệu log/metric nhạy cảm của doanh nghiệp đều không bị rò rỉ ra bên ngoài hay bị dùng để huấn luyện các mô hình công cộng.

---

### 5. KẾT LUẬN

Bài viết từ các chuyên gia AWS đã chứng minh rằng Generative AI không chỉ dùng để viết code hay tạo văn bản, mà còn là một "đồng nghiệp AI" đắc lực trong phòng trực sự cố của các đội ngũ SRE.

---

### 6. TÀI LIỆU THAM KHẢO

- [AWS Machine Learning Blog - Build multi-agent site reliability engineering assistants with Amazon Bedrock AgentCore](https://aws.amazon.com/blogs/machine-learning/build-multi-agent-site-reliability-engineering-assistants-with-amazon-bedrock-agentcore/)
