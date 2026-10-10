## 4. Hướng dẫn thực chiến: Tạo Custom Agent chuyên Backend từ A-Z

Lý thuyết như vậy là đã đủ, bây giờ hãy cùng xắn tay áo lên và tự chế một "đệ tử ruột" chuyên xử lý các tác vụ Backend bằng **Python**. Trong hướng dẫn này, chúng ta sẽ thiết lập một Custom Agent cho một dự án Backend Python tiêu chuẩn dựa trên framework **FastAPI**, tuân thủ nghiêm ngặt cấu trúc phân lớp hiện đại.

### Bước 1: Tạo thư mục cấu hình `.cursor/rules`

Hệ thống Cursor thế hệ mới quản lý các quy tắc thông qua các file Markdown riêng biệt nằm trong một thư mục chỉ định ở gốc dự án.

1. Mở dự án Python của bạn bằng Cursor.
2. Tại thư mục gốc (root directory), hãy tạo một thư mục mới có tên chính xác là: `.cursor/rules/`.
3. Bên trong thư mục này, tạo một file mới đặt tên là `backend-python-rules.md`.

*Mẹo nhỏ:* Bạn có thể tạo nhiều file quy tắc khác nhau (ví dụ: `testing-rules.md`, `db-rules.md`). Cursor sẽ tự động đọc, phân tích và áp dụng tất cả các file cấu hình có đuôi `.md` trong thư mục này tùy theo ngữ cảnh file bạn đang làm việc.

### Bước 2: Viết "Luật pháp" cho Agent (File mẫu)

Hãy copy nội dung cấu hình thực chiến dưới đây và dán vào file `.cursor/rules/backend-python-rules.md` của bạn. Đây là bộ khung tiêu chuẩn giúp AI định hình tư duy của một Senior Python Backend Developer:

```markdown
---
description: Áp dụng khi tạo mới hoặc sửa đổi các thành phần Backend Python bao gồm API, Logic nghiệp vụ, và tương tác Cơ sở dữ liệu.
globs: "app/**/*.py"
---

# Quy chuẩn phát triển Backend Python (FastAPI)

Bạn là một chuyên gia Senior Python Backend Engineer. Khi thực hiện bất kỳ tác vụ nào trong thư mục `app/`, bạn BẮT BUỘC phải tuân thủ nghiêm ngặt các quy tắc cấu trúc và bảo mật dưới đây.

## 1. Kiến trúc mã nguồn (Router - Service - Repository)
Mọi tính năng hoặc API mới phải được phân tách rõ ràng thành các lớp độc lập:
- **Router (Lớp hiển thị):** Chỉ định nghĩa các endpoint của FastAPI, HTTP methods, Status Code và Dependency Injection (`Depends`). Sử dụng **Pydantic** để validate dữ liệu đầu vào/đầu ra (`response_model`). Không viết logic nghiệp vụ tại đây.
- **Service (Lớp nghiệp vụ):** Nơi xử lý logic nghiệp vụ chính (Business Logic). Nhận dữ liệu sạch từ Router, thực hiện tính toán, điều hướng logic và gọi lớp Repository.
- **Repository (Lớp dữ liệu):** Nơi duy nhất được tương tác với Cơ sở dữ liệu thông qua **SQLAlchemy** (sử dụng Async Session) hoặc **SQLModel**. Tuyệt đối không gọi Repository chéo giữa các Service khác nhau.

## 2. Quy chuẩn Code & Bảo mật dữ liệu
- **Type Hints:** Tất cả các hàm bắt buộc phải có Type Hints đầy đủ cho cả tham số đầu vào và kiểu dữ liệu trả về (ví dụ: `def get_user(user_id: int) -> UserSchema:`).
- **An toàn mật khẩu:** Không bao giờ lưu mật khẩu dạng plain text. Phải sử dụng thư viện `passlib` với thuật toán `bcrypt` để hash mật khẩu.
- **Bảo mật SQL:** Luôn sử dụng ORM hoặc Parameterized Queries. Tuyệt đối không dùng f-string hay nối chuỗi để tạo các câu lệnh SQL thô nhằm chặn đứng nguy cơ SQL Injection.
- **Xử lý ngoại lệ:** Sử dụng các khối `try ... except` một cách tường minh. Khi xảy ra lỗi nghiệp vụ, hãy chủ động raise `HTTPException` từ FastAPI với mã trạng thái phù hợp (ví dụ: 400, 404, 403).

## 3. Quản lý môi trường & Thư viện
- Dự án này sử dụng `poetry` để quản lý dependency. Khi cần cài đặt thư viện mới, hãy chạy lệnh `poetry add <package>` trong terminal, tuyệt đối không dùng `pip` hoặc `pipenv`.
```

### Bước 3: Kích hoạt và kiểm thử thành quả

Sau khi lưu file, "bộ não" mới của Agent đã sẵn sàng hoạt động. Hãy cùng kiểm tra xem nó có thực sự lột xác hay không bằng cách yêu cầu nó tạo một tính năng CRUD cơ bản.

1. Nhấn tổ hợp phím `Cmd + I` (trên macOS) hoặc `Ctrl + I` (trên Windows/Linux) để mở **Cursor Composer**.
2. Hãy chắc chắn rằng bạn đã chuyển sang chế độ **Agent** (chữ "Agent" sáng lên ở góc cửa sổ).
3. Nhập vào câu lệnh prompt thử nghiệm sau:
   > *"Hãy tạo cho tôi tính năng CRUD cho thực thể Sản phẩm (Product), bao gồm các trường: tên, giá, và số lượng tồn kho."*

**Đối chiếu kết quả trước và sau khi cấu hình:**
- **Khi chưa cấu hình (Mặc định):** Agent thường sẽ lười biếng viết tất cả các hàm route, schema Pydantic và câu lệnh DB dồn chung vào một file duy nhất kiểu `product.py` để xong việc nhanh chóng, code không hề có Type Hints rõ ràng.
- **Sau khi có `.cursor/rules`:** Agent sẽ tự động tạo cấu trúc folder chuẩn chỉnh: Tạo file schema Pydantic trong `schemas/product.py`, tạo router FastAPI độc lập trong `routers/product.py` tích hợp `Depends`, tạo logic nghiệp vụ trong `services/product.py` và phần truy vấn DB bất đồng bộ (async) trong `repositories/product.py`. Toàn bộ code đều có Type Hints chỉnh chu và tự động dùng `poetry add` nếu phát hiện thiếu thư viện bổ trợ.

Chỉ với vài phút thiết lập, bạn đã cấu hình thành công một Agent chuyên Python Backend hiểu rõ cấu trúc dự án của bạn đến từng dòng code!
