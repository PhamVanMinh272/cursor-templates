## 5. Những "Kỹ năng tối thượng" (Advanced Tips) nên nạp cho Custom Agent

Khi đã làm chủ được các thiết lập cơ bản, bạn có thể "tiến hóa" Custom Agent của mình lên một đẳng cấp khác. Bằng cách bổ sung các quy tắc nâng cao vào thư mục `.cursor/rules/`, bạn sẽ biến Agent từ một người thợ viết code thuần túy thành một kỹ sư tự động hóa toàn diện từ kiểm thử đến quản lý cơ sở dữ liệu.

### Tự động hóa Unit Test với Pytest
Nỗi sợ lớn nhất của dev khi dùng AI là nó sửa được logic này nhưng lại làm hỏng (break) logic khác mà không ai hay biết. Hãy ép Agent phải tự chịu trách nhiệm với đoạn code mình viết ra bằng quy tắc sau:

> **Quy tắc nạp thêm:** *"Mỗi khi thay đổi logic xử lý trong thư mục `app/services/`, bạn bắt buộc phải tìm file test tương ứng trong thư mục `tests/` để cập nhật. Ngay sau đó, hãy tự động mở terminal và chạy lệnh `poetry run pytest`. Nếu kết quả test báo lỗi (Fail), bạn phải tự đọc log lỗi, sửa lại code và chạy lại test cho đến khi Pass hoàn toàn mới được dừng lại."*

Nhờ quy tắc này, Agent sẽ hoạt động như một vòng lặp TDD (Test-Driven Development) tự động. Bạn chỉ cần ngồi uống trà và nhìn AI tự viết code, tự chạy test và tự sửa lỗi cho chính nó.

### Kiểm soát Migration Database nghiêm ngặt với Alembic
Trong các dự án thực tế, việc AI tự ý sửa đổi trực tiếp vào file cấu hình DB cũ (`models.py`) mà không tạo file migration là một thảm họa, dễ làm sập dữ liệu môi trường Staging hoặc Production. Hãy dựng một "hàng rào pháp lý" cho cơ sở dữ liệu:

> **Quy tắc nạp thêm:** *"Tuyệt đối không được chỉnh sửa trực tiếp cấu trúc bảng (schema) trong database mà không qua migration. Khi có sự thay đổi về Model của SQLAlchemy/SQLModel, bạn phải chạy lệnh `poetry run alembic revision --autogenerate -m "tên_migration"` để sinh file mới. Hãy kiểm tra kỹ file migration được tạo ra trong thư mục `alembic/versions/` để đảm bảo không có câu lệnh drop bảng ngoài ý muốn trước khi thông báo hoàn thành."*

Quy trình này giúp lịch sử thay đổi database của dự án luôn sạch sẽ, minh bạch và an toàn tuyệt đối.

### Tích hợp Tài liệu Nội bộ (Internal Docs & Confluence)
Mỗi công ty hoặc dự án đều có những convention (quy ước) "ngầm" hoặc cách thiết kế hệ thống đặc thù mà không một mô hình AI public nào biết được. Cursor cho phép bạn liên kết các tài liệu này để làm "sách giáo khoa" riêng cho Agent.

1. **Sử dụng tính năng `@Docs`:** Trong giao diện Cursor, hãy truy cập vào mục Settings > Features > Docs và nhấn **Add New Doc**. Sau đó, dán URL tài liệu API nội bộ, quy trình deploy, hoặc chuẩn thiết kế hệ thống của công ty bạn vào. Cursor sẽ tự động cào (crawl) và index toàn bộ dữ liệu này.
2. **Kích hoạt trong quy tắc:** Trong file `.cursor/rules/backend-python-rules.md`, bạn thêm một dòng:
   > *"Khi thiết kế các tính năng liên quan đến xác thực hoặc phân quyền, hãy luôn tham chiếu đến kiến trúc được định nghĩa trong tài liệu `@Tên_Tài_Liệu_Của_Bạn` để đảm bảo tính đồng bộ."*

Bằng cách này, Custom Agent không chỉ thông minh hơn mà nó còn thực sự hòa nhập vào môi trường và quy trình làm việc riêng biệt của doanh nghiệp bạn.
