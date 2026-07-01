# Bước 4: Chiến lược dữ liệu (Test Data Strategy)

**Workflow:** `$generate-automation-from-testcases` (tiếp tục)
**Skill:** `$qa-automation-engineer` + `$test-data-generator`

---

## Mục đích

Test automation hay bị flaky nếu dùng dữ liệu cứng (hardcode). Bước này yêu cầu AI thiết kế **bộ sinh dữ liệu ngẫu nhiên** (Faker/Random) mang tính traceable để test chạy nhiều lần / song song không bị trùng lặp.

## Cách sử dụng

1. Gửi file `prompt.txt` cho AI.
2. AI sẽ sinh:
   - Class Utils/DataProvider chứa hàm generate data
   - Hướng dẫn tích hợp vào Test Cases
3. Review và tích hợp vào project → sang Bước 5.

## Format dữ liệu chuẩn

```
[Prefix]_[TestName]_[Timestamp]_[Random]
```

Ví dụ: `auto_createCustomer_20260402_A3F2@test.com`

→ Nhìn database biết ngay: data do test `createCustomer` sinh ra lúc `2026-04-02`.

## Lưu ý

- Mỗi test method có data **riêng biệt** → chạy parallel an toàn.
- Dùng Faker library cho data realistic (tên người, địa chỉ, SĐT...).
- Tuân thủ quy tắc trong `.agents/rules/automation_rules.md` (Section 2: Test Data).
