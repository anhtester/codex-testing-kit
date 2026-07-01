# Prompt Templates

Các prompt templates tái sử dụng cho các tác vụ QA automation phổ biến. Agent có thể tham khảo khi cần format output hoặc khi user cung cấp yêu cầu chưa rõ ràng.

---

## 1. Test Case Generation

```
Phân tích requirement sau và sinh test cases:

**Requirement:** [Mô tả requirement]

**Output format:**
| TC ID | Test Case Title | Precondition | Steps | Expected Result | Priority | Type |

**Yêu cầu:**
- Bao gồm positive, negative, boundary, edge cases
- Sử dụng tiếng Việt cho mô tả
- Priority: High / Medium / Low
- Type: Positive / Negative / Boundary / Edge
```

---

## 2. Automation Script Generation

```
Chuyển đổi test case sau thành automation script:

**Test Case:** [TC content]
**Framework:** [Selenium Java / Playwright TypeScript]
**Pattern:** Page Object Model

**Output:**
1. Page Object class(es)
2. Test class
3. Test data (nếu cần)

**Quy tắc:**
- Smart waits only (không hard sleep)
- Random test data với prefix + timestamp
- Assertions rõ ràng
```

---

## 3. API Test Generation

```
Sinh API tests từ Swagger specification:

**Swagger URL:** [URL]
**Endpoint(s):** [Endpoint cần test]
**Framework:** REST Assured + TestNG

**Bao gồm:**
- Happy path (200 OK)
- Validation errors (400)
- Authentication (401/403)
- Not found (404)
- Boundary values
- Schema validation
```

---

## 4. Locator Generation

```
Inspect element và sinh locator ổn định:

**Element:** [Mô tả element cần tìm]
**Page URL:** [URL]
**Tool:** [Selenium / Playwright]

**Output:**
- Locator chính (primary)
- Locator dự phòng (fallback)
- Giải thích lý do chọn locator
```

---

## 5. Flaky Test Analysis

```
Phân tích test flaky và đề xuất fix:

**Test file:** [Path to test]
**Triệu chứng:** [Mô tả hành vi flaky]

**Phân tích:**
1. Root cause
2. Pattern phát hiện (timing, data, environment, selector)
3. Đề xuất fix cụ thể
4. Code fix
```

---

## 6. Test Data Generation

```
Sinh test data cho module:

**Module:** [Tên module]
**Fields:** [Danh sách fields cần data]

**Bao gồm:**
- Valid data (happy path)
- Invalid data (negative)
- Boundary values (min, max, empty, null)
- Special characters
- Format: JSON / CSV / Excel
```
