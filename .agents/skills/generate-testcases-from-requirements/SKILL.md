---
name: generate-testcases-from-requirements
description: Sinh manual test cases nhanh từ requirements (QUICK mode — không qua quy trình 6 bước).
---

> **BẮT BUỘC (MANDATORY SKILL):** Bạn PHẢI nạp và đọc kỹ nội dung của skill **`$rbt-manual-testing`** (tại `.agents/skills/rbt-manual-testing/SKILL.md`) trước khi bắt đầu thực hiện tác vụ này. Sử dụng **Mode QUICK** của skill.

# Workflow: Sinh Manual Test Cases Nhanh từ Requirements

Workflow này sử dụng **Mode QUICK** của skill `$rbt-manual-testing` để sinh test cases nhanh từ requirements đã sẵn có.

## ⚠️ Nguyên tắc

- **Mode:** QUICK (1 lượt duy nhất, không chờ user giữa chừng)
- Phù hợp cho module đơn giản, requirements đã rõ ràng
- Nếu phát hiện requirements quá phức tạp hoặc mơ hồ → **tự động chuyển sang FULL RBT** và thông báo user
- Tất cả output bằng **Tiếng Việt**

## Các bước thực hiện

1. **Đọc và hiểu requirements** được user cung cấp
2. **Xác định các luồng chính:** Happy Path, Negative Path, Boundary Cases, Edge Cases
3. **Áp dụng kỹ thuật thiết kế test case tự động:**
   - Equivalence Partitioning (EP)
   - Boundary Value Analysis (BVA)
   - Decision Table (nếu có nhiều rules)
   - State Transition (nếu có workflow)
4. **Validation chuyên biệt từng trường (Field-Level Validation - 15 Field Types):**
   - Liệt kê tất cả input fields trên form/UI
   - Sinh validation TCs **riêng cho TỪNG trường** theo đặc tính riêng (Text, Email, Phone, Date, Number, Dropdown, Checkbox/Radio, File Upload, Password, Textarea, OTP/MFA, Date Range, Rich Text, Multi-Select, Range Slider)
   - Áp dụng **Bảng Field-Level Validation Checklist** trong skill `$rbt-manual-testing` để chọn validation phù hợp
   - **KHÔNG** gộp validation nhiều trường vào 1 test case
5. **Bao phủ Scenarios Chuyên Sâu & Non-Functional:**
   - Race Condition / Double Submit (double click nút submit, concurrent edit)
   - Session & Network Resilience (session timeout mid-form, loss of network, slow 3G)
   - Localization & UTF-8 / Emoji (tiếng Việt có dấu, emoji, ký tự đa ngôn ngữ)
   - Keyboard Accessibility (Tab navigation, Enter/Space key, Focus state)
6. **Sinh test cases đầy đủ fields & Metadata Automation:**
   - TC ID (format: `[DỰ_ÁN]_[MODULE]_TC_[SỐ]`)
   - Module, Test Scenario, Pre-conditions, Test Steps, Expected Results, Test Data (cụ thể), Priority
   - Gắn đầy đủ metadata: `Automatable`, `Auto Type`, và `@Tags`
7. **Chạy Self-Quality Gate (5 tiêu chí):** Rà soát lại 100% test cases trước khi xuất kết quả.

## Bảng Output Standard (chuẩn hóa đầy đủ Metadata)

```markdown
| TC ID | Module | Test Scenario | Pre-Condition | Test Steps | Expected Result | Test Data | Priority | Automatable | Auto Type | Tags |
```

> **Giải thích Metadata Automation:**
> - **Automatable:** `Yes` / `No` / `Partial` (Độ khả thi để viết script tự động)
> - **Auto Type:** `UI` / `API` / `Unit` / `N/A` (Loại automation phù hợp)
> - **Tags:** `@Smoke`, `@Regression`, `@CriticalPath`, `@Security`, `@Boundary`

## Quy tắc quan trọng

- Test Data phải cụ thể: `test_login_01@domain.com`, không phải "email hợp lệ"
- Phải bao gồm cả Positive, Negative, Boundary, và Edge cases
- Mỗi trường input phải có validation TCs riêng (không gộp nhiều trường vào 1 TC)
- TC ID theo format thống nhất do user quy ước hoặc mặc định `[DỰ_ÁN]_[MODULE]_TC_[SỐ]`
- Chạy Self-Quality Gate rà soát chất lượng trước khi bàn giao
- Nếu quá nhiều TCs → chia thành Part 1, Part 2 và hỏi user

## Khi nào chuyển sang FULL RBT

Agent **tự động đề xuất chuyển mode** nếu phát hiện:
- Requirements mơ hồ, cần hỏi Q&A
- Scope lớn (>3 modules)
- Logic nghiệp vụ phức tạp, nhiều điều kiện chồng chéo
- User yêu cầu Traceability Matrix hoặc Risk Assessment