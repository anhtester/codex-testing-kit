# Bước 1: Khởi tạo ngữ cảnh (Context & Role-play)

**Workflow:** `$generate-automation-from-testcases`
**Skill:** `$qa-automation-engineer`

---

## Mục đích

Định hình cho AI vai trò **Senior Automation Engineer** và nạp bối cảnh kỹ thuật. Bước này giúp AI biết chính xác:
- Framework nào (Playwright / Selenium / Appium)
- Ngôn ngữ nào (TypeScript / Java)
- Kiến trúc project ra sao
- Các nguyên tắc code phải tuân thủ

## Cách sử dụng

1. Mở file `prompt.txt`.
2. Thay thế các phần trong `[...]`:
   - **Tech Stack:** Chọn framework, ngôn ngữ, build tool
   - **Mục tiêu:** Hệ thống/tính năng cần tự động hóa
   - **Bối cảnh:** Kiến trúc web, công nghệ frontend, đặc thù element
   - **Kiến trúc:** Copy từ `project_architecture/README.md` hoặc mô tả project hiện có
3. Gửi cho AI và chờ xác nhận → sang Bước 2.

## Lưu ý

- Chọn đúng framework từ đầu — AI sẽ sinh code theo cú pháp framework đó xuyên suốt.
- Nếu project đã tồn tại, mô tả cấu trúc hiện có để AI sinh code vào đúng thư mục.
- Bước này chỉ cần chạy **1 lần** đầu conversation.
