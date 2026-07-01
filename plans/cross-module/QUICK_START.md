# 📋 Hướng Dẫn Nhanh: Cross-Module Testing & Ma Trận Kết Hợp

## 🔀 Chọn Luồng Sử Dụng

### Luồng 1: Antigravity (Slash Command) — Tự động (Đề xuất ⭐)

> Dùng khi bạn đang sử dụng **Antigravity** (Google Gemini plugin).

```
$generate-cross-module-test-plan

Tính năng: [Tên tính năng, VD: "Biên bản thanh toán cho đối tác"]
URL: [https://your-app.com]
Tài khoản: [admin@test.com / Test@123]

Các modules liên quan:
1. [Module 1: Quản lý đối tác — chọn loại đối tác]
2. [Module 2: Tạo thanh toán — chọn VND/USD]
3. [Module 3: Cấu hình thuế — chọn loại thuế]
4. [Module 4: Quản lý công nợ — chọn loại công nợ]
5. [Module cuối: Sinh biên bản — output]

Chiến lược ma trận: pairwise (hoặc: business-critical / full-cartesian)
```

→ AI tự mở browser → khám phá từng module → vẽ Data Flow → sinh ma trận kết hợp.

---

### Luồng 2: Copy-Paste vào ChatGPT / Claude — Thủ công

> Dùng khi bạn muốn dùng AI khác (không phải Antigravity).

**Prompt mẫu — Copy paste vào chat AI:**

```
Bạn là Senior QA Engineer chuyên Combinatorial Testing.

Tôi có tính năng "[TÊN TÍNH NĂNG]" đi qua nhiều modules nối tiếp nhau.
Mỗi module có nhiều lựa chọn, và bộ kết hợp các lựa chọn quyết định output cuối.

Các modules và dimensions:
- Module 1 [TÊN]: dimension [TÊN CHIỀU] = [giá trị 1, giá trị 2, ...]
- Module 2 [TÊN]: dimension [TÊN CHIỀU] = [giá trị 1, giá trị 2, ...]
- Module 3 [TÊN]: dimension [TÊN CHIỀU] = [giá trị 1, giá trị 2, ...]
- ...

Hãy thực hiện:
1. Vẽ Data Flow Diagram giữa các modules (module nào output gì → input module nào)
2. Liệt kê tất cả constraints (bộ kết hợp không hợp lệ)
3. Sinh bảng ma trận kết hợp theo chiến lược Pairwise Testing
4. Với mỗi bộ kết hợp, ghi rõ Expected Output (template, công thức nếu có)

Output dạng bảng Markdown, sẵn sàng copy sang Excel.
```

---

## 🎯 Luồng End-to-End — Từng bước

### Bước 1: Phân tích Cross-Module & Sinh Ma Trận

```
$generate-cross-module-test-plan

Tính năng: Biên bản thanh toán cho đối tác
URL: https://example.com/partners
```

**Kết quả:** AI sinh ra:
- 📊 Data Flow Diagram (module nào → module nào)
- 📋 Bảng Dimensions (tất cả chiều + values)
- 📈 **Ma trận kết hợp** (Pairwise ~20 bộ thay vì 216 bộ Full)

**⏸️ User review:** Kiểm tra ma trận → bổ sung/sửa → xác nhận OK.

---

### Bước 2: Sinh Test Data cho Ma Trận

```
$generate-combinatorial-test-data

Ma trận: [paste bảng ma trận từ Bước 1]
Mode: GENERATE (hoặc PIPELINE nếu muốn tạo data thật trên hệ thống)
Format: json (hoặc: csv, markdown, typescript)
```

**Kết quả:**
- Mode GENERATE: File JSON/CSV chứa N bộ data, mỗi bộ = 1 combo
- Mode PIPELINE: AI chạy browser thật → tạo data trên hệ thống → report pass/fail

---

### Bước 3: Sinh Test Cases (Tùy chọn)

```
$generate-manual-testcases-rbt

Requirements: [paste requirements + ma trận kết hợp từ Bước 1]
```

→ AI sinh test cases chi tiết cho từng bộ kết hợp quan trọng.

---

### Bước 4: Sinh Automation Scripts (Tùy chọn)

```
$generate-automation-from-testcases

URL: https://example.com
Test cases: [paste test cases từ Bước 3]
Framework: Playwright TypeScript
```

→ AI sinh scripts + tự chạy + tự fix → PASS stable.

---

## 📊 Ví Dụ Thực Tế: Biên Bản Thanh Toán Đối Tác

### Input (bạn cung cấp):

```
Tính năng: Biên bản thanh toán cho đối tác
Modules:
1. Quản lý Đối tác: Loại = [Tổ chức, Cá nhân, Hộ KD]
2. Thanh toán: Loại = [VND, USD]
3. Thuế: Loại = [PIT, VAT, Nhà thầu, Miễn thuế]
4. Công nợ: Loại = [Thường, Tạm ứng, Điều chỉnh]
5. Nguồn tài sản: Loại = [Quỹ A, Quỹ B, Quỹ C]
```

### Output (AI sinh ra):

**Data Flow:**
```
Đối tác → Thanh toán → Thuế → Công nợ → Biên bản
(type)     (currency)   (Phụ thuộc     (Phụ thuộc
                         type+currency)  tất cả)
```

**Ma trận Pairwise (20 bộ thay vì 3×2×4×3×3 = 216 bộ):**

| # | Đối tác | TT | Thuế | Công nợ | Nguồn | Expected |
|---|---------|------|------|---------|-------|----------|
| 1 | Tổ chức | VND | VAT | Thường | Quỹ A | BB_TC_VND_VAT |
| 2 | Tổ chức | USD | PIT | Tạm ứng | Quỹ B | BB_TC_USD_PIT |
| 3 | Cá nhân | VND | PIT | Thường | Quỹ A | BB_CN_VND_PIT |
| 4 | Cá nhân | USD | VAT | Điều chỉnh | Quỹ C | BB_CN_USD_VAT |
| 5 | Hộ KD | VND | Nhà thầu | Thường | Quỹ B | BB_HKD_VND_NT |
| ... | ... | ... | ... | ... | ... | ... |

→ Cover 100% cặp giữa 2 dimensions bất kỳ, chỉ cần ~20 bộ!

---

## 💡 Mẹo Tối Ưu

1. **Bắt đầu với Pairwise** — đủ tốt cho 90% trường hợp, giảm 80-90% công sức
2. **Cung cấp business rules** nếu có — AI sẽ map vào cột "Expected Output" chính xác hơn
3. **Review Data Flow ở Bước 2** — đây là checkpoint quan trọng nhất, sai ở đây → ma trận sẽ sai
4. **Dùng Mode PIPELINE** khi test data phải tạo thật qua UI (không thể seed database)
5. **Chạy trong cùng 1 conversation** với Antigravity để AI giữ context xuyên suốt
6. **Chia batch** nếu ma trận > 30 bộ — tránh timeout và giữ chất lượng

---

## ⚠️ Phân Biệt: Khi Nào KHÔNG Cần Workflow Này?

| Tình huống | Dùng workflow nào? |
|------------|-------------------|
| Test 1 module đơn lẻ, form đơn giản | `$generate-manual-testcases-rbt` hoặc `$generate-testcases-from-requirements` |
| Nhiều modules nhưng **độc lập** (không ảnh hưởng lẫn nhau) | `$generate-application-test-plan` |
| Nhiều modules **nối tiếp**, output phụ thuộc **bộ kết hợp** | ✅ `$generate-cross-module-test-plan` ← **Dùng workflow này** |
| Chỉ cần test data cho 1 form | `$generate-test-data` |
