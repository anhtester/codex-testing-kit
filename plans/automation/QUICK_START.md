# 📋 Hướng Dẫn Nhanh: Automation Testing 6 Bước

## Hai cách sử dụng

### Cách 1: One-Click (Tự động hoàn toàn — Đề xuất)

```
$generate-automation-from-testcases

URL: [https://your-app.com/login]
Tài khoản: [admin@test.com / Test@123]
Framework: [Playwright TypeScript / Selenium Java]

Manual Test Cases:
[Paste test cases vào đây]
```

→ Agent tự chạy hết 6 bước, tự fix đến khi test PASS.

---

### Cách 2: Tuần Tự (Từng bước)

| Bước | Prompt gửi Antigravity | Chờ User? |
|------|------------------------|-----------|
| **0** | Xem `project_architecture/README.md` | Setup 1 lần |
| **1** | Copy `01.../prompt.txt` + điền `[...]` | ✅ Chờ xác nhận |
| **2** | Copy `02.../prompt.txt` + điền URL & TCs | ✅ Review locators |
| **3** | Copy `03.../prompt.txt` | Review POM |
| **4** | Copy `04.../prompt.txt` | Review nhanh |
| **5** | Copy `05.../prompt.txt` | Chờ test PASS |
| **6** | Copy `06.../prompt.txt` | Nhận clean code |

### Luồng thực hiện:

```
[Bước 1] Thiết lập role + tech stack
    ↓  AI xác nhận → OK
[Bước 2] Cung cấp URL + Test Cases
    ↓  AI tự mở browser, thu thập locators
    ↓  ⏸️ User review bảng locators
[Bước 3] AI thiết kế POM classes
    ↓  User review kiến trúc
[Bước 4] AI sinh Data Generator class
    ↓  User review nhanh
[Bước 5] AI sinh test script + tự chạy
    ↓  Tự fix loop đến khi PASS ✅
[Bước 6] AI cleanup code
    ↓  User nhận clean code → commit ✅
```

---

## Mẹo Tối Ưu

1. **Dùng Cách 1** cho 80% trường hợp — nhanh và hiệu quả nhất
2. **Dùng Cách 2** khi project lớn hoặc cần kiểm soát chi tiết từng module
3. **Luôn chạy trong cùng 1 conversation** để AI giữ context
4. **Cung cấp tài khoản test** nếu app yêu cầu login
