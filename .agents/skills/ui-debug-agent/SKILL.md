---
name: ui-debug-agent
description: Skill inspect web/mobile applications bằng browser tools, phân tích DOM elements, xác định locators ổn định, debug UI automation failures, và hỗ trợ sinh Page Object classes.
---

# UI Debug Agent

## Description

Skill chuyên biệt giúp agent inspect ứng dụng web/mobile trực tiếp trên browser thật, phân tích DOM, thu thập locators ổn định, và debug các vấn đề UI automation.

Agent có thể:

- Mở browser thật, navigate đến bất kỳ URL nào
- Inspect DOM elements — xác định attributes, hierarchy, state
- Thu thập locators ổn định cho Playwright, Selenium, Appium
- Debug automation failures (element not found, click intercepted, timeout)
- Capture UI state (snapshot, screenshot) để phân tích
- Phân tích dynamic content, iframe, shadow DOM, SPA navigation

---

## When to Use

Sử dụng skill này khi:

- Cần **khám phá UI** của một trang web/module mới
- Cần **tìm locator** cho element cụ thể
- Cần **debug** test automation fail do UI thay đổi
- Cần **verify** locator có hoạt động trên DOM thực tế không
- Cần **phân tích DOM** để hiểu cấu trúc UI (forms, tables, modals)
- Cần **capture evidence** (screenshot) cho test report

Trigger keywords: "inspect UI", "tìm locator", "debug element", "mở browser xem", "kiểm tra DOM"

---

## MCP Command Sequence (BẮT BUỘC)

Khi sử dụng Playwright MCP để debug UI, **LUÔN** tuân theo thứ tự:

```
1. browser_navigate(url)           → Mở trang
2. browser_resize(1920, 1080)      → Desktop viewport
3. browser_wait_for(text/time)     → Chờ page load
4. browser_snapshot()              → Thu thập DOM (dùng để phân tích + tìm locator)
5. browser_click/type/hover(ref)   → Tương tác (nếu cần)
6. browser_take_screenshot()       → Chụp ảnh (evidence khi fail hoặc milestone)
```

### Quy tắc quan trọng:

| Quy tắc | Chi tiết |
|---|---|
| **KHÔNG navigate lại** nếu đã ở đúng trang | Tránh reload ngoài ý muốn |
| **LUÔN resize** ngay sau navigate | `browser_resize(1920, 1080)` — đảm bảo desktop viewport |
| **LUÔN wait** trước khi snapshot | Chờ page load hoàn tất |
| **Dùng snapshot để phân tích** | Snapshot trả về accessibility tree — nhanh, chính xác, có `ref` để tương tác |
| **Dùng screenshot để báo cáo** | Screenshot là hình ảnh — dùng khi cần evidence visual |

---

## Snapshot vs Screenshot

| | `browser_snapshot` | `browser_take_screenshot` |
|---|---|---|
| **Trả về** | Accessibility tree (text + ref IDs) | Hình ảnh (PNG/JPEG) |
| **Mục đích** | Phân tích DOM, tìm locator, xác định element | Visual evidence, báo cáo, debug layout |
| **Khi nào dùng** | ⭐ Luôn dùng trước khi tương tác | Chỉ khi fail hoặc milestone quan trọng |
| **Có ref để interact** | ✅ Có — dùng ref để click/type/hover | ❌ Không — chỉ là hình ảnh |
| **Tốc độ** | Nhanh | Chậm hơn |

**Quy tắc:** Ưu tiên `snapshot` cho phân tích, dùng `screenshot` cho evidence.

---

## Quy trình Inspect UI

### 1. Mở & Chuẩn bị trang

```
browser_navigate → URL target
browser_resize → 1920 × 1080
browser_wait_for → chờ indicator page đã load (text hoặc thời gian)
```

Nếu trang yêu cầu đăng nhập:
- Hỏi user credentials HOẶC dùng fixture sẵn có trong project
- **KHÔNG đọc file `.env` trực tiếp** (quy tắc bảo mật)

### 2. Thu thập DOM Structure

```
browser_snapshot → accessibility tree
```

Từ snapshot, xác định:
- **Các element chính:** buttons, inputs, links, headings, tables
- **Attributes quan trọng:** role, name, label, placeholder, testid
- **Hierarchy:** parent → child relationships
- **State:** visible, enabled, disabled, checked, expanded

### 3. Xác định Locators

Với mỗi element cần locator, áp dụng **priority order** theo framework:

**Playwright:**

| Priority | Locator | Ví dụ | Khi nào dùng |
|---|---|---|---|
| 1 ⭐ | `getByRole()` | `getByRole('button', {name: 'Submit'})` | Element có role + accessible name rõ ràng |
| 2 | `getByLabel()` | `getByLabel('Email')` | Form input có label |
| 3 | `getByPlaceholder()` | `getByPlaceholder('Enter email')` | Input có placeholder, không có label |
| 4 | `getByText()` | `getByText('Welcome back')` | Text content unique |
| 5 | `getByTestId()` | `getByTestId('submit-btn')` | Element có data-testid attribute |
| 6 | CSS | `page.locator('.submit-button')` | Không có semantic option nào phù hợp |
| 7 | XPath | `page.locator('//div[@class="x"]')` | Last resort — tránh dùng |

**Selenium:**

| Priority | Locator | Ví dụ |
|---|---|---|
| 1 ⭐ | `By.id()` | `By.id("email")` |
| 2 | `By.cssSelector("[data-testid]")` | `By.cssSelector("[data-testid='submit']")` |
| 3 | `By.name()` | `By.name("username")` |
| 4 | `By.cssSelector()` | `By.cssSelector(".login-form button")` |
| 5 | `By.xpath()` | `By.xpath("//button[text()='Login']")` |

**Appium (Mobile):**

| Priority | Locator | Ví dụ |
|---|---|---|
| 1 ⭐ | Accessibility ID | `MobileBy.accessibilityId("loginButton")` |
| 2 | ID (resource-id) | `MobileBy.id("com.app:id/login_btn")` |
| 3 | Name | `MobileBy.name("Login")` |
| 4 | XPath (relative) | `MobileBy.xpath("//android.widget.Button[@text='Login']")` |

### 4. Verify Locator

Sau khi xác định locator, **bắt buộc verify** trên DOM thực tế:

```
browser_snapshot → tìm element bằng ref
browser_click/type(ref) → thử tương tác
browser_snapshot → xác nhận kết quả
```

**Locator được chấp nhận khi:**
- [ ] Unique trên page (chỉ match 1 element)
- [ ] Ổn định qua nhiều lần reload
- [ ] Không chứa dynamic class (css-xxx, sc-xxx, MuiXxx-root)
- [ ] Không chứa positional xpath (//div[3]/button[2])
- [ ] Không phụ thuộc auto-generated attribute

---

## Xử lý tình huống đặc biệt

### Trang yêu cầu đăng nhập
- Dùng fixture login sẵn có trong project hoặc hỏi user credentials
- **KHÔNG đọc .env trực tiếp**
- Sau khi login, navigate đến trang cần inspect

### Modal / Dialog / Popup
- Modal thường là overlay trên page chính
- `browser_snapshot` sẽ thấy modal content trong accessibility tree
- Tương tác với modal elements bằng ref từ snapshot
- Chờ modal animation hoàn thành trước khi interact

### Iframe
- `browser_snapshot` có thể không thấy content trong iframe
- Dùng `browser_evaluate` để switch vào iframe:
  ```javascript
  () => document.querySelector('iframe').contentDocument.body.innerHTML
  ```
- Hoặc dùng Playwright frame locator: `page.frameLocator('#iframe-id')`

### Shadow DOM
- Playwright `locator()` tự động pierce shadow DOM
- Selenium cần `shadowRoot.findElement()`
- `browser_snapshot` có thể thấy shadow DOM content tùy MCP version

### Dynamic Content (SPA / AJAX)
- Chờ content load bằng `browser_wait_for(text)` trước khi snapshot
- Nếu content load lazy → scroll xuống trước, rồi snapshot
- Nếu content thay đổi theo thời gian → chụp snapshot nhiều lần

### Tables / Lists (nhiều elements lặp)
- Xác định pattern locator cho row/cell
- Dùng `nth()` hoặc `filter()` để target element cụ thể
- Ví dụ Playwright: `page.getByRole('row').filter({hasText: 'John'}).getByRole('button', {name: 'Edit'})`

### Element bị che (Overlay / Toast)
- Kiểm tra z-index, opacity, visibility trong DOM
- Chờ overlay biến mất: `browser_wait_for(textGone: 'Loading...')`
- Nếu toast notification che button → chờ toast timeout

---

## Anti-Patterns (FORBIDDEN)

| ❌ Sai | ✅ Đúng | Lý do |
|---|---|---|
| Đoán locator từ tên tính năng | Inspect DOM thực tế rồi mới lấy locator | Locator chính xác 100% |
| Dùng screenshot để chọn locator | Dùng snapshot (accessibility tree) | Snapshot có ref, screenshot thì không |
| Copy locator từ code cũ không verify | Luôn verify locator trên browser hiện tại | DOM có thể đã thay đổi |
| Dùng dynamic class `.css-1abc` | Dùng role/label/testid | Dynamic class thay đổi mỗi build |
| Dùng positional xpath `//div[3]` | Dùng relative xpath hoặc CSS | Positional xpath dễ vỡ |
| Chụp screenshot liên tục | Chỉ screenshot khi fail hoặc milestone | Tốn resource, chậm |
| Navigate lại khi đã ở đúng trang | Chỉ navigate khi cần đổi URL | Tránh reload không cần thiết |

---

## Output

Skill này có thể trả về:

- **Locator recommendations** — bảng primary + fallback cho mỗi element
- **DOM analysis** — cấu trúc element, attributes, state, hierarchy
- **Page Object suggestions** — class structure phù hợp cho trang đã inspect
- **Screenshots** — evidence visual tại các milestone
- **Debug findings** — nguyên nhân element not found / click fail + cách fix

---

## Rules References

Agent PHẢI tuân thủ các rules chi tiết:

- `.agents/rules/locator_strategy.md` — Master locator priority map
- `.agents/rules/playwright_rules.md` — Playwright browser setup and locator rules
- `.agents/rules/selenium_rules.md` — Selenium locator and wait rules
- `.agents/rules/appium_rules.md` — Appium mobile locator rules
- `.agents/rules/automation_rules.md` — General automation best practices