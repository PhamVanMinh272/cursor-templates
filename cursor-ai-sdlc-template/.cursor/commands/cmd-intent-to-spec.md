---
description: Chuyển đổi ý tưởng thô thành đặc tả kỹ thuật chi tiết cho AWS Lambda.
command: /spec
---

Hãy đọc tệp ý tưởng `@docs/intent.md`. Dựa trên codebase hiện tại của dự án, hãy tự động sinh ra (hoặc cập nhật) tệp `@docs/spec.md`.

Yêu cầu đặc tả rõ ràng về mặt kỹ thuật cho AWS Lambda Python:
1. Xác định rõ Trigger loại nào (API Gateway Proxy hay SQS Batch)?
2. Liệt kê các API Endpoints mới hoặc cấu trúc SQS message schema.
3. Ràng buộc dữ liệu đầu vào và các lỗi (Error Handling) cần bắt.
4. KHÔNG viết code logic ở bước này.
