# Bản đồ các chế độ trong Cursor và Giới hạn của thiết lập mặc định

Để hiểu tại sao chúng ta cần một Custom Agent, trước hết hãy cùng nhìn lại bức tranh tổng thể về hệ sinh thái AI bên trong Cursor. Không giống như các extension hỗ trợ AI thông thường, Cursor phân tách các tác vụ lập trình thành 3 chế độ (mode) cốt lõi với mức độ tự chủ tăng dần. Việc chọn đúng chế độ cho từng tác vụ là chìa khóa đầu tiên để làm chủ công cụ này.

### 1. Inline Edit (Tổ hợp phím `Cmd/Ctrl + K`)
Đây là chế độ can thiệp nhanh và trực tiếp nhất. Bạn chỉ cần bôi đen một đoạn code hoặc đặt con trỏ chuột tại dòng mong muốn, nhấn phím tắt và đưa ra yêu cầu. AI sẽ chỉnh sửa hoặc viết thêm mã nguồn ngay tại chỗ. 
*   **Điểm mạnh:** Cực kỳ nhanh, phản hồi tức thì.
*   **Tác vụ phù hợp:** Viết một hàm tiện ích ngắn, refactor nhanh tên biến, bổ sung comment/JSDoc, hoặc sửa một lỗi cú pháp hiển nhiên.

### 2. Chat mode (Tổ hợp phím `Cmd/Ctrl + L`)
Giao diện này hoạt động giống như một trợ lý tư vấn truyền thống (tương tự ChatGPT hay Claude) hiển thị ở thanh Sidebar. Điểm khác biệt là Chat mode của Cursor có khả năng đọc và hiểu ngữ cảnh của file bạn đang mở hoặc toàn bộ codebase (khi dùng tính năng `@Codebase`). AI sẽ trả về câu trả lời và các đoạn code mẫu trong cửa sổ chat.
*   **Điểm mạnh:** An toàn tuyệt đối vì AI không tự ý can thiệp vào file gốc. Nó đóng vai trò như một người bạn đồng hành để thảo luận giải pháp.
*   **Tác vụ phù hợp:** Hỏi đáp kiến thức công nghệ mới, giải thích các thuật toán phức tạp, hoặc nhờ phân tích một đoạn log lỗi dài mà bạn dán vào.

### 3. Agent mode (Tổ hợp phím `Cmd/Ctrl + I`)
Đây là đỉnh cao công nghệ của Cursor và cũng là chế độ đã được thiết lập làm mặc định (default) trong các phiên bản gần đây. Thay vì đứng ngoài quan sát, Agent mode hoạt động theo một vòng lặp tự chủ (Autonomous Loop): Nghiên cứu codebase ➡️ Lập kế hoạch ➡️ Tự động tạo và sửa đổi hàng loạt file ➡️ Chạy Terminal để kiểm thử ➡️ Tự sửa lỗi nếu lệnh build/test thất bại.
*   **Điểm mạnh:** Khả năng tự động hóa toàn diện từ đầu đến cuối một tính năng phức tạp mà không cần dev phải copy-paste thủ công.

---

## Nỗi đau từ Agent mặc định: Khi "Junior" làm việc lớn

Mặc dù Agent mode sở hữu quyền năng rất lớn, nhưng nếu bạn chỉ sử dụng nó ở cấu hình mặc định (default), bạn sẽ sớm đối mặt với những "cơn ác mộng" đặc trưng của một Backend Developer khi làm việc trong các dự án thực tế:

*   **Sự mù tịt về kiến trúc hệ thống (Architectural Blindness):** Mỗi dự án Backend đều có một triết lý thiết kế riêng, có thể là Clean Architecture, DDD (Domain-Driven Design), hay MVC truyền thống. Agent mặc định không hề biết điều đó. Khi bạn yêu cầu *"Viết API đăng ký người dùng"*, nó có thể nhét thẳng logic xử lý database vào file Controller, phá vỡ hoàn toàn cấu trúc phân lớp (Layers) mà team của bạn đã mất công xây dựng.
*   **Lỗ hổng bảo mật và Quy chuẩn Database:** AI mặc định có xu hướng chọn giải pháp dễ nhất để chạy được. Nó sẵn sàng viết các câu lệnh SQL thô (raw SQL) thay vì dùng ORM của dự án, bỏ qua các bước mã hóa mật khẩu, hoặc validate dữ liệu đầu vào cực kỳ lỏng lẻo. Đối với dự án Backend, đây là những quả bom hẹn giờ về bảo mật.
*   **Cơn ác mộng "Prompt Fatigue":** Để Agent mặc định làm đúng ý, bạn sẽ rơi vào vòng lặp mệt mỏi khi phải liên tục gõ đi gõ lại các câu lệnh rập khuôn: *"Nhớ dùng pnpm chứ không dùng npm nhé"*, *"Hãy viết Unit Test bằng Jest và kiểm tra kỹ case này nhé"*, *"Tạo file migration mới chứ đừng sửa schema cũ nhé"*. 

Chính vì những giới hạn này, việc để Agent mode chạy tự do ở thiết lập mặc định giống như giao toàn bộ hệ thống cho một lập trình viên học việc năng nổ nhưng thiếu kinh nghiệm. Để đưa Agent lên một đẳng cấp mới, chúng ta cần xây dựng cho nó một "bộ khung luật pháp" riêng — đó chính là lúc Custom Agent xuất hiện.
