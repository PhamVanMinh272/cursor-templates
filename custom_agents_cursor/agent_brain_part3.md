## 3. "Bộ não" của Custom Agent: File `.cursor/rules` hoạt động ra sao?

Nếu coi **Agent mode** là một cỗ máy có động cơ cực kỳ mạnh mẽ, thì hệ thống quy tắc **`.cursor/rules`** chính là vô lăng và hệ thống định vị giúp cỗ máy đó đi đúng hướng. Để biến Cursor mặc định thành một trợ lý Senior thực thụ, bạn cần hiểu rõ cơ chế vận hành bên dưới của "bộ não" này.

### Định nghĩa bản chất: Khi Agent Mode kết hợp với `.cursor/rules`

Bản chất của một **Custom Agent** trong Cursor không phải là một mô hình AI mới do bạn tự huấn luyện từ đầu. Thực chất, đó là sự kết hợp cộng hưởng giữa:
*   **Năng lực thực thi mạnh mẽ của Agent Mode:** Khả năng tự đọc file, tự viết code, tạo file mới và chạy terminal.
*   **Hành lang pháp lý từ `.cursor/rules`:** Tập hợp các file cấu hình bằng ngôn ngữ tự nhiên (Markdown) quy định kiến trúc, tiêu chuẩn code và quy trình làm việc mà AI **bắt buộc** phải tuân theo.

Khi chưa có cấu hình, Agent giống như một lập trình viên freelance mới toe, vào dự án là tự ý viết code theo thói quen riêng. Nhưng khi bạn đưa `.cursor/rules` vào, AI sẽ lập tức hiểu được "văn hóa" và "luật lệ" của codebase hiện tại.

### Cơ chế hoạt động: Cách Cursor nạp quy tắc vào "Harness"

Mỗi khi bạn kích hoạt Chat hoặc Agent Mode (qua tổ hợp phím `Cmd/Ctrl + L` hoặc `Cmd/Ctrl + I`), một quy trình ngầm sẽ được Cursor thực hiện như sau:

*   **Bước 1 - Quét tự động (Scanning):** Cursor sẽ tự động tìm kiếm thư mục `.cursor/rules/` ở gốc dự án. Nó sẽ đọc tiêu đề, mô tả và các điều kiện kích hoạt (glob patterns) của từng file `.md` trong đó.
*   **Bước 2 - Bơm ngữ cảnh (Context Injection):** Trước khi gửi yêu cầu (prompt) của bạn lên Server AI, Cursor sẽ nạp toàn bộ nội dung quy tắc phù hợp vào **"Harness"** (bộ khung điều phối hệ thống). Các quy tắc này đóng vai trò như một lớp *System Prompt* ẩn, tối cao và có độ ưu tiên lớn nhất.
*   **Bước 3 - Định hình hành vi (Behavior Shaping):** AI sẽ tiếp nhận yêu cầu của bạn nhưng dưới góc nhìn của bộ quy tắc. Ví dụ, nếu bạn bảo *"Tạo cho tôi API Login"*, thay vì viết một hàm lộn xộn trong một file duy nhất, AI sẽ nhớ luật: *"À, dự án này dùng Clean Architecture, mình phải tạo Controller, Service, và dùng bcrypt để hash pass như quy định trong file `.cursor/rules`"*.

Nhờ cơ chế này, bạn không cần phải lặp đi lặp lại những câu lệnh dài dòng ở mỗi lần chat. Mọi tiêu chuẩn đã được "đóng đinh" sẵn vào tư duy của Agent ngay từ vạch xuất phát.