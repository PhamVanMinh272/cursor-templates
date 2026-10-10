# Quy trình làm việc (Workflow) tối ưu với AI Coding Agent (Cursor) dành cho Python Developer

Là một **Python Software Developer**, việc chuyển đổi từ tư duy *"bảo AI viết hộ code"* sang tư duy *"làm việc với một Pair Programmer / Tech Lead"* sẽ giúp bạn khai thác tối đa sức mạnh của Cursor. Dưới đây là nội dung chi tiết để bạn thiết lập và vận hành workflow chuẩn mực.

---

## 1. Thiết lập "Bộ nhớ" và Quy tắc cho dự án (Project Rules)

Để Cursor không phải đoán cấu trúc code Python của bạn mỗi lần chat, hãy định nghĩa sẵn các quy tắc bằng file cấu hình riêng:

*   **Tạo file quy tắc:** Tạo thư mục `.cursor/rules/` trong dự án của bạn và tạo các file `.mdc` hoặc file quy tắc chung như `AGENTS.md` / `CLAUDE.md`.
*   **Nội dung cần khai báo:**
    *   **Tech stack Python cụ thể:** Ví dụ: Python 3.12, FastAPI, SQLAlchemy async, Pydantic v2, Pytest.
    *   **Quy chuẩn code:** Định nghĩa rõ quy chuẩn PEP 8, bắt buộc dùng `ruff` hoặc `black`, và yêu cầu ghi type hints cho mọi function.
    *   **Cấu trúc thư mục:** Layered architecture, quy định rõ folder chứa domain logic và folder chứa infrastructure.
    *   **Lệnh chạy mặc định:** Khai báo lệnh chạy test/lint cố định (Ví dụ: `pytest`, `ruff check .`).

---

## 2. Chuẩn hoá Workflow qua 5 bước thực thi task

Khi giao một nhiệm vụ cho Cursor Agent (Composer / Agent mode), hãy áp dụng quy trình 5 bước sau:

### Bước 1: Lập kế hoạch trước (Plan First)
*   **Hành động:** Đừng bắt AI viết code ngay lập tức. Yêu cầu Agent đọc codebase và lên kế hoạch (plan) trước.
*   **Prompt mẫu:** *"Hãy phân tích yêu cầu [X], kiểm tra các file liên quan, và đề xuất một kế hoạch thực hiện ngắn gọn trước khi viết code."*

### Bước 2: Kiểm chứng bằng Unit Test (Test-Driven Development)
*   **Hành động:** Với Python, việc bảo Agent viết test cùng lúc (ví dụ dùng `pytest`) giúp bạn kiểm chứng logic nhanh chóng và chính xác hơn.

### Bước 3: Cho Agent tự chạy Terminal & Tự sửa lỗi
*   **Hành động:** Tận dụng khả năng tích hợp terminal của Cursor. Sau khi sinh code, hãy bảo nó tự chạy lệnh test hoặc lệnh lint (`ruff`). Nếu có lỗi, AI sẽ tự đọc stack trace và tự sửa cho đến khi tất cả bài test đều pass.

### Bước 4: Review Code theo Checklist cụ thể
*   **Hành động:** Tuyệt đối không nhìn lướt qua rồi bấm Accept toàn bộ. Hãy bôi đen phần diff và bắt Agent tự kiểm tra lại theo các tiêu chí:
    *   **Bảo mật:** Check SQL injection, leak secret, lộ thông tin cấu hình.
    *   **Hiệu năng:** Check lỗi query N+1 trong SQLAlchemy, tối ưu bộ nhớ.
    *   **Chất lượng:** Đảm bảo Clean Code và xử lý tốt các edge cases (trường hợp biên).

### Bước 5: Bắt AI "Dạy lại" (Knowledge Transfer)
*   **Hành động:** Sau khi hoàn thành một task khó, hãy đặt câu hỏi để nắm vững giải pháp.
*   **Prompt mẫu:** *"Hãy giải thích tại sao em chọn giải pháp này và có edge case nào anh cần lưu ý khi scale hệ thống này lên không?"*

---

## 3. Kiểm soát bảo mật và rủi ro

*   **Không để lộ tệp nhạy cảm:** Tạo file `.cursorignore` tương tự `.gitignore` để ẩn các file chứa API key, file cấu hình `.env`, dữ liệu khách hàng hoặc các thư mục log tạm thời.
*   **Giữ quyền kiểm soát (Human-in-the-loop):** Hãy luôn nhớ bạn là Architect, AI chỉ là người thực thi. Bạn là người chịu trách nhiệm cuối cùng về kiến trúc tổng thể và business logic của dự án.