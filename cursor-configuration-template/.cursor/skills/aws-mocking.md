# Kỹ năng Mock AWS Services bằng Moto/Pytest

**Description:** Kích hoạt khi người dùng yêu cầu viết Unit Test, Integration Test cho Lambda Function hoặc các hàm gọi qua Boto3.

## Hướng dẫn Mocking cho Agent:
1. Luôn sử dụng thư viện `pytest` và `moto` (để mock SQS, DynamoDB, S3).
2. Viết các `pytest.fixture` để khởi tạo mock environment trước khi chạy test.
3. Khi test SQS Handler: Tự tạo một mock event có cấu trúc `{"Records": [{"body": "...", "messageId": "..."}]}` để truyền vào handler.
4. Khi test API Gateway Handler: Mock cấu trúc `{"body": "...", "headers": {...}, "requestContext": {...}}`.
