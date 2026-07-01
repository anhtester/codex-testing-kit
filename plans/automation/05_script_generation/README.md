# Bước 5: Sinh mã Automation (Script Generation)

**Workflow:** `$generate-automation-from-testcases` (tiếp tục)
**Skill:** `$qa-automation-engineer`

---

## Mục đích

Bước cốt lõi — AI kết hợp POM (Bước 3) và Data Strategy (Bước 4) để sinh file Test script hoàn chỉnh, chạy test, và tự sửa nếu fail.

## Cách sử dụng

1. Gửi file `prompt.txt` cho AI.
2. AI sẽ:
   - Sinh file Test script hoàn chỉnh
   - **Tự chạy test** bằng terminal
   - Nếu fail → **tự đọc log, tự sửa, tự chạy lại**
   - Lặp đến khi PASS ổn định
3. Khi test PASS → sang Bước 6.

## Code Pattern: Arrange → Act → Assert

```
Arrange: Setup data, khởi tạo pages
Act:     Thực hiện hành động
Assert:  Kiểm tra kết quả
```

## Self-fix Loop (Tự sửa)

AI thực hiện vòng lặp:
```
Sinh code → Chạy test → FAIL?
    ├── Đọc error log
    ├── Phân tích root cause
    ├── Sửa code
    └── Chạy lại → PASS? → DONE ✅
```

## Lưu ý

- AI sẽ **không hỏi user** trong quá trình self-fix (trừ khi gặp business rule mâu thuẫn).
- Smart Waits bắt buộc — xem `.agents/rules/playwright_rules.md` hoặc `.agents/rules/selenium_rules.md`.
- Mỗi test case phải có **assertion rõ ràng** ở cuối.
