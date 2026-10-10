# Tiêu đề bài viết: Vượt qua giới hạn của Cursor mặc định: Sức mạnh từ Custom Agent tự chế

---

## 1. Mở bài (Intro)
*   **Đặt vấn đề:** Thừa nhận sức mạnh của Cursor Agent mặc định trong việc tiết kiệm thời gian, tự sửa code và chạy terminal. Tuy nhiên, khi làm dự án Backend thực tế, Agent mặc định bắt đầu lộ giới hạn như viết sai cấu trúc folder, tạo file Migration không đúng chuẩn, hoặc viết Unit Test sơ sài.
*   **Giải pháp:** Để thực sự tối ưu hiệu suất, Backend Dev cần tự tay thiết lập một Custom Agent nhằm biến nó từ một "Junior học việc" thành một "Senior hiểu rõ codebase".
*   **Lời hứa bài viết:** Bài viết này sẽ hướng dẫn từng bước cách vượt qua các giới hạn mặc định để tự chế một Agent chuyên xử lý các tác vụ Backend phức tạp.

---

## 2. Bản đồ các chế độ trong Cursor và Giới hạn của thiết lập mặc định
*   **Tổng quan hệ sinh thái AI của Cursor:** Phân loại nhanh 3 chế độ cốt lõi dựa trên mức độ tự chủ tăng dần của AI:
    *   *Inline Edit (Cmd/Ctrl + K):* Sửa nhanh tại chỗ trong một file, phù hợp với các hàm ngắn hoặc đổi tên biến.
    *   *Chat mode (Cmd/Ctrl + L):* Trình tư vấn, giải thích thuật toán, chỉ trả về code mẫu trong cửa sổ chat để dev tự copy-paste.
    *   *Agent mode (Cmd/Ctrl + I):* Trợ lý tự chủ cao nhất, có khả năng tự sửa nhiều file cùng lúc và tự chạy Terminal.
*   **Nỗi đau từ Agent mặc định (The Pain Point):** Dù Agent mode là mạnh nhất, nhưng nếu để ở cấu hình mặc định (default), nó sẽ gặp các giới hạn lớn khi làm Backend:
    *   *Thiếu ngữ cảnh kiến trúc:* AI không biết dự án đang dùng Clean Architecture, DDD, hay MVC để tuân thủ.
    *   *Lỗi bảo mật và Quy chuẩn:* AI dễ sinh ra các đoạn code vi phạm quy tắc bảo mật như validate lỏng lẻo hoặc viết câu lệnh SQL thô dễ dính Injection.
    *   *Mất thời gian sửa đổi (Prompt Fatigue):* Lập trình viên phải liên tục gõ lại các câu lệnh nhắc nhở quen thuộc như "Hãy viết Unit Test bằng Jest" hoặc "Nhớ tạo file migration mới".

---

## 3. "Bộ não" của Custom Agent: File `.cursor/rules` hoạt động ra sao?
*   **Định nghĩa bản chất:** Giải thích ngắn gọn cơ chế hoạt động của Custom Agent trong Cursor thực chất là sự kết hợp giữa Agent Mode và hệ thống quy tắc `.cursor/rules`.
*   **Cách Cursor đọc file cấu hình:** Mỗi khi bạn gọi Agent, nó sẽ tự động nạp các quy tắc này vào "Harness" (bộ khung điều phối) để định hình hành vi trước khi tự chỉnh sửa file hay chạy Terminal.

---

## 4. Hướng dẫn thực chiến: Tạo Custom Agent chuyên Backend từ A-Z
*   **Bước 1: Tạo thư mục cấu hình:** Hướng dẫn tạo folder `.cursor/rules/` ngay tại thư mục gốc của dự án backend.
*   **Bước 2: Viết "Luật pháp" cho Agent:** Minh họa file mẫu `.cursor/rules/backend-rules.md` quy định cấu trúc code API bắt buộc đi qua các lớp (Controller, Service, Repository), quy định an toàn dữ liệu, và quy định Package Manager khi cài thư viện mới.
*   **Bước 3: Kích hoạt và kiểm thử:** Hướng dẫn mở Composer bằng phím tắt, bật chế độ Agent, ra lệnh thử nghiệm tạo một API CRUD và đối chiếu kết quả trước/sau khi cấu hình.

---

## 5. Những "Kỹ năng tối thượng" (Advanced Tips) nên nạp cho Custom Agent
*   **Tự động hóa Unit Test:** Ép Agent cứ mỗi lần sửa logic ở Service là phải tự chạy lệnh kiểm thử để kiểm tra, nếu tạch test thì tự sửa lại code.
*   **Kiểm soát Migration Database:** Yêu cầu Agent không được sửa trực tiếp file Schema cũ mà phải luôn tạo file migration mới theo định dạng thời gian chuẩn.
*   **Tích hợp Tài liệu Nội bộ (Internal Docs):** Hướng dẫn đưa tài liệu API hoặc quy trình Deploy của công ty vào làm tài liệu tham khảo cho Agent.

---

## 6. Kết luận & Kêu gọi hành động (Call to Action)
*   **Tóm tắt bài viết:** Việc bỏ ra 15 phút để cấu hình Custom Agent ban đầu sẽ giúp bạn tiết kiệm hàng giờ đồng hồ sửa code rác của AI về sau.
*   **Lời khuyên cốt lõi:** Đừng xem Agent là một công cụ thay thế bạn, hãy biến nó thành một "đệ tử ruột" được bạn huấn luyện bài bản.
*   **Kêu gọi hành động (CTA):** Bạn đã thử tạo `.cursor/rules` cho dự án của mình chưa? Hãy chia sẻ cấu hình tâm đắc nhất của bạn ở phần bình luận bên dưới nhé!
