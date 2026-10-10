---
description: Đóng vai Tech Lead tự review lại phần code diff vừa viết để tìm lỗ hổng.
command: /review
---

Hãy đóng vai một AWS Serverless Tech Lead nghiêm khắc. Hãy đối chiếu phần code diff bạn vừa chỉnh sửa với tài liệu gốc `@docs/spec.md`.

Tiến hành rà soát và báo cáo ngắn gọn cho tôi:
1. **Serverless Best Practices:** Khởi tạo Boto3 Client đã đúng chỗ chưa? Có nguy cơ gây Cold start không? Có dùng lệnh `print()` nào thay vì module `logging` không?
2. **Lambda Gateway / SQS:** Cấu hình Response format đã chuẩn proxy chưa? Vòng lặp SQS Records đã có try/catch để tránh crash cả batch chưa?
3. **Bảo mật:** Có dấu hiệu leak cứng AWS Credentials hoặc API Key nào không?
