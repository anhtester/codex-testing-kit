# Bước 3: Thiết kế cấu trúc POM (POM Design)

**Workflow:** `$generate-automation-from-testcases` (tiếp tục)
**Skill:** `$qa-automation-engineer`

---

## Mục đích

Sau khi AI đã thu thập locators từ DOM thật ở Bước 2, bước này hướng dẫn AI định hình các **Class Page** theo chuẩn POM. Mục tiêu là phân bổ đúng file, tên hàm có ý nghĩa rõ ràng **trước khi** cài logic test.

## Cách sử dụng

1. Đảm bảo đã review và xác nhận locators từ Bước 2.
2. Gửi file `prompt.txt` cho AI.
3. AI sẽ phác thảo:
   - Tên class Page + file path
   - Locator declarations (từ Bước 2)
   - Method signatures + body
4. Review kiến trúc POM → sang Bước 4.

## Quy tắc đặt tên

| Thành phần | Quy tắc | Ví dụ |
|---|---|---|
| **Class name** | PascalCase + hậu tố `Page` | `LoginPage`, `CustomerFormPage` |
| **Locator** | camelCase, mô tả element | `emailInput`, `submitButton` |
| **Method** | camelCase, mô tả hành động nghiệp vụ | `fillLoginForm()`, `verifySuccessToast()` |
| **File** | Theo convention framework | `LoginPage.ts` / `LoginPage.java` |

## Lưu ý

- Bước này chỉ thiết kế **Page classes**, CHƯA sinh test script.
- Method nên return `this` hoặc target Page (fluent pattern) để chain được.
- Tuân thủ quy tắc trong `.agents/rules/automation_rules.md`.
