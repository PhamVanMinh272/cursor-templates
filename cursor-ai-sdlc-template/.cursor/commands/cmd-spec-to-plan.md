---
description: Lập kế hoạch can thiệp file và kịch bản test dựa trên spec.
command: /plan
---

Hãy chuyển sang **Plan Mode**. Đọc kỹ tệp đặc tả `@docs/spec.md`. 
Quét toàn bộ codebase hiện tại và tạo (hoặc cập nhật) tệp `@docs/plan.md` làm checklist công việc.

Nội dung `plan.md` bắt buộc phải bao gồm:
1. **Affected Files:** Danh sách chính xác các file `.py` cần tạo mới hoặc chỉnh sửa (bao gồm cả file handler và file utils).
2. **Testing Strategy:** Các kịch bản Unit Test (sử dụng pytest và `moto` để mock AWS nếu cần) tương ứng với spec.
3. **Serverless Risks:** Cảnh báo về Cold start (nếu khởi tạo boto3 sai chỗ) hoặc nguy cơ quá hạn Lambda Timeout.
