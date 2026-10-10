# Blueprint: Quy trình làm việc AI-Native SDLC với Cursor AI

Tài liệu này đặc tả quy trình phát triển phần mềm chuẩn AI-native kết hợp giữa triết lý của Anthropic và các tính năng mạnh mẽ của Cursor Agent (Composer mode). Quy trình này thay thế việc gõ prompt thủ công bằng việc giao tiếp và kiểm soát chất lượng qua các tệp Markdown (.md) đóng vai trò làm "Hợp đồng Artifacts".

---

## 🧱 BƯỚC 0: THIẾT LẬP BỘ KHUNG DỰ ÁN (SETUP)

### 1. Cấu trúc thư mục Artifacts
Tạo sẵn thư mục `docs/` tại thư mục gốc của dự án để lưu vết toàn bộ chuỗi tư duy:
- `docs/intent.md` (Ý tưởng ban đầu từ con người)
- `docs/spec.md` (Đặc tả kỹ thuật do AI sinh, con người duyệt)
- `docs/plan.md` ( Checklist công việc chi tiết trước khi code)

### 2. Cấu hình file luật tự động `.cursorrules`
Tạo file `.cursorrules` tại thư mục gốc dự án (hoặc dán vào mục **Features** -> **Project Rules** trong Settings của Cursor) để thiết lập tư duy nền cho Agent:

```markdown
# AI-Native SDLC Rules for Python Project

## Context & Tech Stack
- Language: Python 3.12+ (Yêu cầu strict type hinting cho tất cả các hàm)
- Linter/Formatter: Ruff (Sử dụng lệnh `ruff check --fix .` và `ruff format .`)
- Testing Framework: Pytest (Sử dụng lệnh `pytest`)

## AI-Native SDLC Process (Mandatory)
Bạn bắt buộc phải tuân thủ quy trình phát triển AI-native sau đây cho mọi task:

1. **Không code ngay lập tức:** Khi nhận task, tuyệt đối không được sửa đổi mã nguồn ngay. Hãy đọc các file ngữ cảnh trong thư mục `docs/` để lập kế hoạch trước.
2. **Quyền hạn Terminal (Feedback Loop):** Bạn có toàn quyền mở terminal để tự chạy linter và unit test. Nếu phát hiện lỗi hoặc sai định dạng code, bạn phải tự đọc log và tự sửa lỗi ngầm (Autonomous Mode). Không được dừng lại hỏi user những lỗi cú pháp hoặc lỗi test thông thường.
3. **Tiêu chuẩn hoàn thành:** Task chỉ được coi là hoàn thành khi toàn bộ test suite chuyển sang màu XANH và không còn lỗi linter nào.
```

---

## 🔄 QUY TRÌNH 4 GIAI ĐOẠN PHÁT TRIỂN (4-PHASE WORKFLOW)

Mỗi khi có tính năng hoặc task mới, hãy mở **Cursor Composer (Cmd + I / Ctrl + I)** ở chế độ **Agent** và thực hiện tuần tự theo kịch bản prompt sau:

### 📝 Giai đoạn 1: Khởi tạo ý tưởng (Intent to Spec)
- **Hành động của bạn:** Viết nhanh các gạch đầu dòng mô tả tính năng hoặc lỗi cần sửa bằng ngôn ngữ tự nhiên vào file `docs/intent.md`.
- **Prompt gửi Cursor Agent:**
  > `@docs/intent.md Hãy đọc file ý tưởng này. Dựa trên codebase hiện tại của dự án, hãy tự động sinh ra (hoặc cập nhật) file @docs/spec.md để đặc tả chi tiết về mặt kỹ thuật: các API endpoints nào cần tạo/sửa, cấu trúc Database thay đổi ra sao, và các ràng buộc nghiệp vụ (business logic).`
- **Chốt kết quả:** Đọc file `spec.md` do AI tạo ra để kiểm tra xem nó có hiểu đúng nghiệp vụ không. Chỉnh sửa nếu cần.

### 🗺️ Giai đoạn 2: Kế hoạch thực thi (Spec to Plan)
- **Hành động của bạn:** Yêu cầu Agent chuyển từ tài liệu thiết kế sang danh sách công việc cụ thể.
- **Prompt gửi Cursor Agent:**
  > `@docs/spec.md Hãy chuyển sang Plan Mode. Quét toàn bộ codebase để xác định chính xác các file mã nguồn sẽ bị can thiệp. Tạo file @docs/plan.md liệt kê: danh sách file cần sửa/tạo mới, các kịch bản Unit Test (pytest) cần viết, và các rủi ro hệ thống (side-effects) tiềm ẩn.`
- **Chốt kết quả:** Phê duyệt (Accept) file `plan.md`. File này chính là "bức tường bảo vệ" giữ cho AI không code lan man sang các phần không liên quan.

### 🤖 Giai đoạn 3: Thực thi tự động hoàn toàn (Plan to Code)
- **Hành động của bạn:** Kích hoạt chế độ tự chủ (Autonomous Mode) để AI tự làm việc. Bạn có thể rảnh tay làm việc khác.
- **Prompt gửi Cursor Agent:**
  > `@docs/plan.md Hãy thực thi kế hoạch này ở chế độ Agent. Hãy viết các file unit test bằng pytest trước (Test-Driven), sau đó viết code logic để pass các bài test đó. Sau khi code xong, hãy tự mở terminal chạy lệnh test và ruff để format lại code. Nếu test bị lỗi (đỏ), hãy tự đọc log và tự debug sửa code cho đến khi toàn bộ hệ thống XANH hoàn toàn.`
- **Chốt kết quả:** Ngồi quan sát Cursor tự động mở terminal, chạy lệnh, đọc lỗi và sửa code cho tới khi hoàn tất 100%.

### 🧐 Giai đoạn 4: Đánh giá & Tiếp nhận (Review & Knowledge Transfer)
- **Hành động của bạn:** Đóng vai trò làm chốt chặn Tech Lead để kiểm soát chất lượng code cuối cùng trước khi commit.
- **Prompt gửi Cursor Agent:**
  > `Code đã pass test thành công. Bây giờ hãy đóng vai một vị Tech Lead nghiêm túc, đối chiếu phần code diff em vừa làm với tài liệu gốc @docs/spec.md. Hãy tự phản biện và chỉ ra cho tôi các điểm lưu ý quan trọng về mặt hiệu năng (ví dụ: lỗi N+1 query, async bottlenecks) hoặc bảo mật nếu có.`
- **Chốt kết quả:** AI chỉ ra các lưu ý, bạn kiểm tra lại lần cuối. Sau đó thực hiện commit toàn bộ mã nguồn kèm theo chuỗi file `.md` trong thư mục `docs/` lên Git để lưu lại vết lịch sử (Audit Trail).

---

## 💡 BÍ KÍP VẬN HÀNH THỰC TẾ TRÊN CURSOR

1. **Luôn tạo nhánh Git (Branch) riêng:** Trước khi kích hoạt Giai đoạn 3, hãy đảm bảo bạn đang ở một branch feature riêng biệt. Nếu Agent hoạt động quá đà làm rối loạn mã nguồn, bạn chỉ cần gõ `git reset --hard` để khôi phục trạng thái ban đầu sạch sẽ.
2. **Chia nhỏ bài toán (Granularity):** Đừng đưa một yêu cầu quá lớn vào file `intent.md`. AI-native SDLC hoạt động mượt mà và chính xác nhất khi một chuỗi task được giải quyết gọn gàng trong vòng 1-2 tiếng làm việc của con người.
3. **Cập nhật quy tắc liên tục:** Nếu trong quá trình chạy, bạn phát hiện Cursor thường xuyên mắc một lỗi lập trình cố định (ví dụ: quên đóng kết nối DB, dùng sai phiên bản thư viện), hãy cập nhật ngay lỗi đó vào mục `## Lưu ý tránh lỗi` của file `.cursorrules`. Bộ nhớ dự án của AI sẽ ngày một thông minh hơn qua từng task.
