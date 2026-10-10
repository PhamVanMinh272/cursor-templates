---
description: Kích hoạt Agent tự động viết code, chạy test và sửa lỗi cho đến khi pass 100%.
command: /execute
---

Hãy chuyển sang chế độ **Agent tự chủ**. Đọc tệp kế hoạch `@docs/plan.md` và thực thi toàn bộ checklist trong đó:

1. **Test-Driven:** Viết hoặc bổ sung các file unit test bằng `pytest` trước.
2. **Logic Implementation:** Viết code logic Python 3.12 tuân thủ nghiêm ngặt các tiêu chuẩn AWS Lambda (Boto3 ngoài global scope, logging request_id, dùng Type Hinting).
3. **Autonomous Feedback Loop:** Tự động mở Terminal của Cursor và chạy các lệnh:
   - `pytest` (hoặc lệnh test tương ứng của dự án như `poetry run pytest`).
   - `ruff check --fix .` (để dọn dẹp format code).
4. **Auto-Debug:** Nếu Terminal báo test đỏ hoặc linter lỗi, hãy tự đọc log và sửa lại code cho đến khi hệ thống XANH 100%. Không dừng lại hỏi user cho các lỗi cú pháp thông thường.
