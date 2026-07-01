# AI-DRIVEN AUTOMATION TESTING FRAMEWORK

**Mục tiêu:** 
Sử dụng AI để tự động hóa quá trình xây dựng Automation Framework, thiết kế POM và sinh code chất lượng cao — dễ bảo trì, CI/CD friendly.

## 📌 Nguyên Tắc Cốt Lõi

1. **AI DOM Recon First:** AI phải sử dụng browser MCP (Playwright/Selenium) để tự mở trình duyệt, inspect DOM thật. TUYỆT ĐỐI không đoán locator.
2. **POM Architecture:** Mọi script tuân thủ Page Object Model — phân tách rõ Pages và Tests.
3. **Smart Waits & Stability:** Không hard sleep (`Thread.sleep`, `waitForTimeout`). Chỉ dùng auto-waiting.
4. **Deterministic Data:** Test data unique + traceable, không hardcode.
5. **Self-fix Loop:** AI tự chạy test → nếu fail → tự đọc log, sửa code, chạy lại → đến khi PASS.

---

## 🚀 Quy Trình 6 Bước + Bước 0 (Setup)

| Bước | Tên | Mục đích | Skill |
|------|-----|----------|-------|
| **0** | Project Architecture | Setup kiến trúc thư mục chuẩn | `$qa-automation-engineer` |
| **1** | Context & Role-play | Thiết lập vai trò + tech stack | `$qa-automation-engineer` |
| **2** | Analysis & UI Recon | AI tự mở browser, thu thập locators | `$qa-automation-engineer` + `$ui-debug-agent` |
| **3** | POM Design | Thiết kế class Page Objects | `$qa-automation-engineer` |
| **4** | Test Data Strategy | Sinh class Data Generator | `$qa-automation-engineer` + `$test-data-generator` |
| **5** | Script Generation | Sinh test script + tự chạy + tự fix | `$qa-automation-engineer` |
| **6** | Review & Refactoring | Clean code + CI/CD readiness | `$qa-automation-engineer` |

*(Mỗi bước tương ứng 1 thư mục con, gồm `README.md` + `prompt.txt`)*

---

## 🎯 Chiến Lược Thực Thi

### Cách 1: Tuần Tự (Manual Control)

Sử dụng thủ công từng file `prompt.txt` (01 → 06):
- **Phù hợp khi:** Chỉ cần AI làm 1 bước cụ thể (VD: "Chỉ sinh POM, không cần test script")
- **Hoặc khi:** Project lớn, muốn kiểm soát tỉ mỉ từng module

### Cách 2: One-Click Auto Workflow (Đề xuất)

Gọi workflow `$generate-automation-from-testcases` + đính kèm Test Cases:
- Agent tự: Đọc TC → Mở Browser → Lấy Locator → Sinh POM → Sinh Script → Chạy Test → Sửa Bug → Đến khi PASS
- **Ưu điểm:** Toàn bộ tự động sau 1 lệnh duy nhất

---

## 📋 Rules tham chiếu

- `.agents/rules/automation_rules.md` — POM, Data, Naming conventions
- `.agents/rules/locator_strategy.md` — Thứ tự ưu tiên locator
- `.agents/rules/playwright_rules.md` — Playwright-specific rules
- `.agents/rules/selenium_rules.md` — Selenium-specific rules
- `.agents/rules/appium_rules.md` — Appium-specific rules

## 📁 Hướng dẫn nhanh

Xem file `QUICK_START.md` trong thư mục này để bắt đầu nhanh.
