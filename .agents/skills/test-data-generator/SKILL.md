---
name: test-data-generator
description: Skill sinh test data có cấu trúc, unique, traceable cho automation tests, bao gồm positive, negative, boundary và edge cases.
---

# Test Data Generator

Purpose: Generate reliable test data for automation tests.

---

## When to Use

Use this skill when:

- Creating test data for new test cases
- Generating boundary and edge case data
- Setting up data-driven tests
- Creating API request payloads

---

## Responsibilities

Generate test data for:

- Registration forms
- Login credentials
- Form submissions
- API payloads
- Search queries
- File uploads

---

## Data Rules

All generated data must be:

- **Unique** — No duplication within test suite
- **Deterministic** — Same seed produces same data (when needed)
- **Traceable** — Can identify which test generated it

---

## Unique Data Pattern

Recommended format:

```
<prefix>_<testName>_<timestamp>
```

Examples:

```
auto_register_20260402133000
test_login_1712024100
```

---

## Common Data Types

### Email
```
auto_<testName>_<timestamp>@test.com
```
Example: `auto_register_20260402@test.com`

### Username
```
user_<testName>_<timestamp>
```
Example: `user_login_20260402133000`

### Phone
```
Random 10-digit number starting with valid prefix
```
Example: `0912345678`

### Password
```
Mix of uppercase, lowercase, digits, special chars
```
Example: `Test@12345`

---

## Data Categories

### Positive Data (Happy Path)
- Valid format, within constraints
- All required fields filled
- Standard business values

### Negative Data
- Missing required fields
- Invalid format (wrong email, short password)
- Invalid characters
- Already existing values (duplicate check)

### Boundary Values
- Minimum length (e.g., 1 character)
- Maximum length (e.g., 255 characters)
- Min + 1, Max - 1
- Empty string vs null
- Zero, negative numbers

### Edge Cases
- Unicode / special characters
- Very long strings
- SQL injection patterns (for security testing)
- HTML tags in text fields
- Leading/trailing whitespace

---

## Constraints

Test data must:

- Respect field validation rules (from DOM inspection)
- Match input format (date format, phone format)
- Avoid duplication across test runs
- Not contain real PII (personal data)

---

## Output Format

Provide data in structured format:

```json
{
  "positive": [
    { "email": "auto_tc01_20260402@test.com", "password": "Test@12345" }
  ],
  "negative": [
    { "email": "", "password": "Test@12345", "expectedError": "Email is required" },
    { "email": "invalid-email", "password": "Test@12345", "expectedError": "Invalid email format" }
  ],
  "boundary": [
    { "email": "a@b.co", "password": "12345678", "note": "Min length" }
  ]
}
```

---

## Multi-Step Data Pipeline (Cross-Module)

> Mở rộng cho bài toán: test data cần đi qua **nhiều modules nối tiếp** mới tạo ra được data hoàn chỉnh cho module cuối.

### Khi nào dùng

- Tính năng đi qua chuỗi N modules (VD: Đối tác → Thanh toán → Thuế → Biên bản)
- Data module sau **phụ thuộc** output module trước (Reference fields)
- Cần tạo data thật trên hệ thống qua browser

### Data Chain Pattern

```
Module 1 → Output: {id_1, code_1}
    ↓ (Reference)
Module 2 → Input: {id_1} → Output: {id_2}
    ↓ (Reference)
Module 3 → Input: {id_1, id_2} → Output: {id_3}
    ↓ (Reference)
Module N → Input: {id_1..id_N-1} → Output: Final Result
```

### Field Classification

| Loại field | Mô tả | Cách sinh data |
|-----------|-------|----------------|
| **Dimension field** | Giá trị thuộc chiều kết hợp trong ma trận | Lấy chính xác từ bộ combo — KHÔNG random |
| **Supporting field** | Bắt buộc nhưng không phải dimension | Random + unique + traceable |
| **Reference field** | ID/code từ output module trước | Copy từ output module trước trong chuỗi |
| **Computed field** | Tự tính từ formula/business rules | Tính theo formula — phải verify |

### Data Chain Tracing Format

```
auto_combo{XX}_{module_short}_{timestamp}
```

Ví dụ cho combo 01:
```
Module 1: partner_name  = "auto_c01_partner_1712049200"
Module 2: payment_desc  = "auto_c01_payment_1712049200"
Module 3: tax_note      = "auto_c01_tax_1712049200"
→ Có thể trace: combo 01 tạo ra những data nào ở mỗi module
```

---

## Combinatorial Data Generation

> Sinh bộ data cho **ma trận kết hợp đa chiều** — mỗi bộ kết hợp = 1 bộ data hoàn chỉnh.

### Khi nào dùng

- Đã có ma trận kết hợp (từ `$generate-cross-module-test-plan`)
- Cần sinh N bộ data tương ứng N bộ kết hợp
- Mỗi bộ data phải có expected output (template, formula, computed values)

### Combinatorial Data Structure

```json
{
  "combination_id": "COMBO_01",
  "dimensions": {
    "D1": "value_from_matrix",
    "D2": "value_from_matrix"
  },
  "module_data": {
    "module_1": { "field1": "...", "field2": "..." },
    "module_2": { "ref_from_module1": "...", "field3": "..." }
  },
  "expected_output": {
    "template": "EXPECTED_TEMPLATE_CODE",
    "formula": "Amount × Rate",
    "computed_values": { "total": 110000000 }
  }
}
```

### Rules cho Combinatorial Data

| # | Rule |
|---|------|
| 1 | Dimension values PHẢI đúng 100% so với ma trận — KHÔNG random |
| 2 | Mỗi combo dùng data riêng (unique per combo) |
| 3 | Computed values phải đúng theo formula |
| 4 | Mỗi combo PHẢI có expected output |
| 5 | Traceable: prefix `auto_combo{XX}` |

### Workflow tham chiếu

- `$generate-cross-module-test-plan` → Sinh ma trận kết hợp (input cho skill này)
- `$generate-combinatorial-test-data` → Workflow chính dùng skill này cho combinatorial data

---

## Rules References

- `.agents/rules/automation_rules.md` — Test data generation rules (Section 2)