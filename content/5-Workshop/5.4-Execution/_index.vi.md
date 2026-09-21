---
title: "Hiện thực chương trình"
date: 2026-06-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### 1. Giao Diện Đăng Nhập, Đăng Ký & Xác Thực Email Qua Amazon SES

Hệ thống cung cấp cơ chế xác thực người dùng an toàn với giao thức mã hóa HTTPS và chứng chỉ SSL từ AWS Certificate Manager. Người dùng có thể đăng nhập bằng tài khoản hiện có hoặc đăng ký tài khoản mới và nhận mã xác thực qua hòm thư điện tử được xử lý tự động bởi dịch vụ Amazon Simple Email Service:

1. Mở trình duyệt web và truy cập địa chỉ: **[https://ericmai.io.vn](https://ericmai.io.vn)**.
2. Kiểm tra biểu tượng khóa bảo mật SSL trên thanh địa chỉ và tiến hành đăng nhập bằng tài khoản người dùng đã tạo.
3. Khi đăng ký tài khoản mới hoặc gửi yêu cầu quên mật khẩu, hệ thống tự động gọi Amazon SES để chuyển tiếp email chứa mã xác thực OTP về hòm thư Gmail của người dùng.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/login.jpg" alt="Giao diện đăng nhập hệ thống ChatPulse" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.26: Giao diện trang Đăng nhập và xác thực tài khoản người dùng tại tên miền ericmai.io.vn</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/register.jpg" alt="Giao diện đăng ký tài khoản người dùng" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.27: Giao diện hoàn tất đăng ký tài khoản người dùng mới trên hệ thống</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/verification_gmail.jpg" alt="Email xác thực tài khoản từ Amazon SES" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.28: Hộp thư Gmail hiển thị email xác thực tài khoản gửi tự động thông qua Amazon SES</p>
</div>

---

### 2. Quản Lý Kết Bạn & Khung Hồ Sơ Tìm Kiếm Người Dùng

Tính năng quản lý danh bạ cho phép người dùng dễ dàng tìm kiếm bạn bè qua số điện thoại, xem chi tiết hồ sơ cá nhân và theo dõi trạng thái hoạt động:

1. **Tìm kiếm người dùng bằng số điện thoại:** Nhập số điện thoại trên thanh công cụ tìm kiếm để lọc tài khoản chính xác theo thời gian thực.
2. **Khung xem hồ sơ cá nhân:** Nhấp vào kết quả tìm kiếm để hiển thị thẻ hồ sơ bao gồm ảnh đại diện avatar, tiểu sử bio, số điện thoại, giới tính và ngày sinh, đồng thời cung cấp tính năng chặn hoặc bỏ chặn người dùng.
3. **Quản lý danh sách bạn bè:** Gửi lời mời kết bạn và đồng ý yêu cầu. Danh bạ hiển thị chấm tròn xanh báo hiệu người dùng đang trực tuyến với dữ liệu đồng bộ từ Redis cache có độ trễ dưới 15ms.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/profile_friend.jpg" alt="Khung tìm kiếm người dùng và hồ sơ cá nhân" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.29: Khung tìm kiếm người dùng bằng số điện thoại hiển thị hồ sơ cá nhân gồm avatar, bio, số điện thoại, giới tính, ngày sinh và tùy chọn chặn hoặc bỏ chặn</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/list_friend.jpg" alt="Danh sách bạn bè và trạng thái trực tuyến" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.30: Danh sách bạn bè với trạng thái trực tuyến được cập nhật tự động theo thời gian thực</p>
</div>

---

### 3. Nhắn Tin Trò Chuyện, Gửi Hình Ảnh & Tệp Tin Thời Gian Thực

Kênh truyền thông thời gian thực là tính năng trọng tâm của ChatPulse, được xây dựng trên giao thức WebSocket Socket.io kết hợp cùng dịch vụ lưu trữ đối tượng đám mây Amazon S3:

1. **Nhắn tin văn bản hai chiều:** Trao đổi tin nhắn tức thời với độ trễ thấp mà không cần tải lại trình duyệt web, hiển thị trạng thái tin nhắn đã gửi và đã nhận.
2. **Tải lên tệp đính kèm an toàn:** Trình duyệt xin cấp quyền tải lên bằng chữ ký bảo mật ngắn hạn S3 Pre-signed URL từ backend, sau đó truyền trực tiếp tệp tin lên Amazon S3 Bucket nhằm tối ưu tốc độ và giảm áp lực tải cho máy chủ EC2.
3. **Hiển thị trực quan và lưu trữ:** Hệ thống demo gửi trực tiếp một tệp tài liệu định dạng PDF trong luồng hội thoại, cho phép người nhận nhấp để xem hoặc tải về an toàn, đồng thời đối tượng tệp tin được lưu trữ bảo mật trên Amazon S3 Bucket.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/messages_real-time_upload_file.jpg" alt="Nhắn tin thời gian thực và gửi tệp PDF đính kèm" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.31: Giao diện nhắn tin trực tiếp hiển thị nội dung hội thoại và tệp tài liệu PDF được gửi thành công</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/bucket_file.jpg" alt="Amazon S3 Bucket lưu trữ đối tượng tệp tin tải lên" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.32: Amazon S3 Bucket lưu trữ an toàn các đối tượng tệp tin tải lên từ ứng dụng ChatPulse</p>
</div>

---

### 4. Cuộc Gọi Thoại & Gọi Video Trực Tiếp Qua WebRTC

Hệ thống tích hợp giải pháp WebRTC thông qua máy chủ LiveKit SFU độc lập, đảm bảo luồng âm thanh và hình ảnh đạt độ phân giải cao cùng độ trễ cực thấp:

1. **Khởi tạo cuộc gọi:** Nhấp vào biểu tượng cuộc gọi trong khung trò chuyện để bắt đầu kết nối tới người nhận.
2. **Màn hình chuông báo cuộc gọi:** Màn hình người gọi hiển thị trạng thái đang đổ chuông kết nối trong khi người nhận xuất hiện thông báo tiếp nhận cuộc gọi.
3. **Phòng gọi video hai chiều:** Khi kết nối thành công, màn hình mở rộng không gian phòng gọi hiển thị đồng thời camera của hai bên với chất lượng hình ảnh sắc nét và âm thanh đồng bộ.
4. **Thanh điều khiển:** Cung cấp đầy đủ các nút bật tắt micro, bật tắt camera, đổi góc nhìn và kết thúc cuộc gọi an toàn.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/calling.jpg" alt="Màn hình đang quay số kết nối cuộc gọi" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.33: Màn hình khởi tạo cuộc gọi hiển thị thông tin người nhận và trạng thái đang kết nối</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/in_call.jpg" alt="Giao diện cuộc gọi video trực tiếp" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.34: Giao diện cuộc gọi video WebRTC hai chiều trực tiếp với âm thanh và hình ảnh độ trễ thấp</p>
</div>

---

### 5. Trợ Lý AI Thông Minh & Trợ Năng Giọng Nói Amazon Polly

ChatPulse nâng tầm trải nghiệm giao tiếp nhờ sự kết hợp giữa mô hình trí tuệ nhân tạo tạo sinh và dịch vụ tổng hợp giọng nói chất lượng cao trên nền tảng đám mây:

1. **Trò chuyện cùng Trợ lý AI:** Người dùng có thể đặt câu hỏi hoặc yêu cầu tóm tắt thông tin ngay trong khung trò chuyện, trợ lý AI sẽ tự động phân tích và phản hồi câu trả lời thông minh, chuẩn xác.
2. **Tổng hợp giọng nói Text-to-Speech với Amazon Polly:**
   - Cạnh các đoạn tin nhắn có biểu tượng loa phát âm.
   - Khi nhấp vào biểu tượng, hệ thống gửi nội dung văn bản tới dịch vụ **Amazon Polly** trên AWS.
   - Amazon Polly xử lý và trả về luồng âm thanh giọng đọc tự nhiên, cho phép phát âm thanh trực tiếp trên trình duyệt web.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/polly.jpg?v=2" alt="Trợ lý AI và tính năng phát giọng nói Amazon Polly" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Hình 5.35: Tương tác với Trợ lý AI và trải nghiệm tính năng phát giọng đọc tin nhắn qua Amazon Polly</p>
</div>

---

### 6. Video Clip Demo Chương Trình

Dưới đây là video clip ghi lại toàn bộ quá trình trải nghiệm và tương tác thực tế với ứng dụng ChatPulse:

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.15); margin: 25px 0;">
  <iframe 
    src="https://www.youtube.com/embed/br8FXBzj4Yk" 
    title="Video Demo Hệ Thống ChatPulse" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
    allowfullscreen>
  </iframe>
</div>
