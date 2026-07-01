# Bước 2: Phân tích & Điều tra UI (Analysis & UI Recon)

**Workflow:** `$generate-automation-from-testcases` (tiếp tục)
**Skill:** `$qa-automation-engineer` + `$ui-debug-agent`

---

## Mục đích

Thay vì con người phải thủ công Inspect DOM, bước này giao nhiệm vụ cho AI **tự mở trình duyệt**, điều hướng web và trích xuất locators thật từ DOM. Đây là bước phân biệt chất lượng giữa automation "đoán mò" và automation "inspect thật".

## Cách sử dụng

1. Điền URL, tài khoản test và Test Cases vào file `prompt.txt`.
2. Gửi cho AI — AI sẽ sử dụng Playwright/Selenium MCP để:
   - Tự khởi động browser
   - Điều hướng theo test steps
   - Thu thập locators từ DOM thật
3. Review bảng locators AI trả về.
4. Nếu locator nào chưa đúng → yêu cầu AI re-inspect element đó.
5. Xác nhận → sang Bước 3.

## Lưu ý quan trọng

- AI sẽ dùng **Accessibility Tree** và **DOM inspection** để tìm locator — không đoán.
- Nếu cần đăng nhập, cung cấp tài khoản test trong prompt.
- Viewport mặc định **1920x1080** (desktop) theo quy tắc trong rules.
- AI ưu tiên locator theo thứ tự trong `.agents/rules/locator_strategy.md`.
