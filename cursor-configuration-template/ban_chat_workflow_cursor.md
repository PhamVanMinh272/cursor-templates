# Bản chất của Workflow trong Cursor AI

Nhận định của bạn **chính xác một nửa**, nhưng phần còn lại đã được cập nhật bằng các tính năng rất mạnh mẽ. 

Bản chất **Cursor AI không có một cái "nút" hay giao diện cố định mang tên "Workflow"** để bạn bấm vào. Thay vào đó, Cursor cung cấp một hệ sinh thái gồm các **Tính năng chủ động (Agent, Composer)** kết hợp với các **Công cụ tùy biến (Rules, Skills, Commands)**. Sự kết hợp này tạo ra các chuỗi quy trình làm việc tự động (AI Workflows) cực kỳ linh hoạt.

---

## 1. Cách các thành phần phối hợp tạo nên một Workflow

Thay vì xây dựng một công cụ Workflow cứng nhắc, Cursor phân rã quy trình thành các khối tư duy và hành động khác nhau:

### Định hình hành vi (Hệ thống quy tắc)
* **Rules (`.cursor/rules/*.mdc`):** Đóng vai trò là "Luật pháp" mang tính bị động. AI sẽ luôn đọc và tuân thủ các quy tắc này (về style code, thư viện, kiến trúc) xuyên suốt mọi tác vụ mà không cần bạn phải nhắc lại.

### Kích hoạt hành động (Lệnh và Kỹ năng)
* **Commands (`/` hoặc `@`):** Là các đoạn prompt phím tắt do bạn tự định nghĩa cho các tác vụ lặp đi lặp lại mang tính thủ công (ví dụ: `/review-code`, `/fix-bug`). AI sẽ không tự gọi lệnh này nếu bạn không yêu cầu.
* **Skills (`SKILL.md`):** Đây là các gói quy trình nhiều bước, có tính "chủ động". Agent của Cursor có thể tự động nhận diện khi nào cần dùng một Skill nào đó để giải quyết bài toán phức tạp, hoặc bạn có thể chỉ định trực tiếp.

### Bộ máy thực thi (Engine)
* **Agent Mode & Composer (`Cmd + L` / `Cmd + I`):** Đây chính là **"Trái tim" của mọi workflow**. Khi bạn ra lệnh, Agent sẽ tự động lập kế hoạch (**Plan Mode**), chỉnh sửa đồng loạt hàng chục file (**Act Mode**), tự mở terminal chạy thử nghiệm (như chạy `npm run test` hoặc `git status`), và tự sửa lỗi nếu test thất bại.

---

## 2. Tính năng Tự động hóa quy trình (Automations)

Cursor hỗ trợ tính năng **Cursor Automations** (hay Cloud Agents). Tính năng này cho phép bạn thiết lập các workflow chạy ngầm trên đám mây dựa theo lịch trình (Cron) hoặc sự kiện (Triggers):
* **Trigger:** Khi có một Pull Request mới trên GitHub hoặc có thông báo lỗi từ Sentry.
* **Action (Workflow tự động):** Cloud Agent của Cursor tự động nhảy vào đọc code, phân tích rủi ro bảo mật, chạy test coverage, viết báo cáo tổng hợp rồi gửi thẳng về kênh Slack của đội ngũ.

> **Tóm lại:** Bạn không thiết lập workflow bằng cách kéo thả sơ đồ, mà bạn thiết lập thông qua việc cấp **Vốn kiến thức (Skills)**, **Luật lệ (Rules)** cho **AI Agent**, và để Agent tự động vận hành chuỗi công việc từ A-Z.


https://www.ibuildwith.ai/blog/cursor-rules-skills-and-commands-oh-my-when-to-use-each/