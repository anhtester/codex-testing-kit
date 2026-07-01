# AI-DRIVEN CROSS-MODULE TESTING FRAMEWORK

**Mục tiêu:**
Phân tích và kiểm thử các tính năng phức tạp đi qua **nhiều modules nối tiếp nhau**, trong đó output phụ thuộc vào **bộ kết hợp điều kiện đa chiều** (Combinatorial Testing).

## 📌 Bài Toán Giải Quyết

Khi một tính năng **KHÔNG nằm gọn trong 1 module** mà phải đi qua chuỗi modules, với mỗi module có nhiều lựa chọn — và bộ kết hợp các lựa chọn quyết định output cuối cùng (template, công thức, business rules khác nhau).

**Ví dụ thực tế:**

| Tính năng | Các chiều kết hợp (dimensions) |
|-----------|------|
| Biên bản thanh toán đối tác | Loại đối tác × Loại thanh toán × Thuế × Công nợ × Nguồn tài sản |
| Hợp đồng bảo hiểm | Loại BH × Đối tượng × Gói × Kỳ hạn × Phương thức TT |
| Đơn hàng xuất khẩu | Thị trường × Loại hàng × Vận chuyển × Thanh toán × Chứng từ |
| Quy trình phê duyệt | Loại yêu cầu × Phòng ban × Cấp × Số tiền → Flow phê duyệt khác nhau |

**Nếu mỗi chiều có 3-5 giá trị →** Tổ hợp Full Cartesian dễ dàng lên **hàng trăm bộ kết hợp**.

---

## 🚀 Quy Trình 2 Giai Đoạn

### Giai đoạn 1: Phân Tích & Sinh Ma Trận (`$generate-cross-module-test-plan`)

| Bước | Tên | Mô tả | Chờ User? |
|------|-----|-------|-----------|
| **1** | Multi-Module Recon | AI mở browser khám phá từng module, thu thập fields + values | ❌ |
| **2** | Data Flow Mapping | Xác định module A output gì → input module B | ✅ **Checkpoint** |
| **3** | Dimension Extraction | Liệt kê tất cả "chiều" kết hợp + values + constraints | ❌ |
| **4** | Combinatorial Matrix | Sinh ma trận kết hợp (Pairwise / Business-critical / Full) | ❌ |
| **5** | Expected Output Mapping | Map expected template + công thức cho mỗi bộ | ✅ **Checkpoint** |

**Output chính:** Bảng ma trận kết hợp — sẵn sàng import Excel/Jira.

### Giai đoạn 2: Sinh Test Data (`$generate-combinatorial-test-data`)

| Mode | Khi nào dùng | Output |
|------|-------------|--------|
| **GENERATE** | Sinh data offline (JSON/CSV/Code) | File test data có cấu trúc |
| **PIPELINE** | Chạy thật qua browser tạo data trên hệ thống | Data thật + IDs + screenshots |

---

## 3 Chiến Lược Ma Trận

| Chiến lược | Mô tả | Khi nào dùng | Ví dụ |
|-----------|-------|-------------|-------|
| **Pairwise** (Mặc định) | Cover 100% cặp giữa 2 dimensions bất kỳ | Tổ hợp lớn (>50) | 216 bộ → ~20 bộ |
| **Business-Critical** | Chỉ chọn bộ quan trọng nhất theo risk | Cần focus, thời gian hạn chế | 216 bộ → ~10 bộ |
| **Full Cartesian** | Test TẤT CẢ tổ hợp hợp lệ | Hệ thống critical (tài chính, y tế) | 216 bộ → 216 bộ |

> 💡 **Pairwise Testing** giảm 80-90% số bộ kết hợp mà vẫn phát hiện phần lớn lỗi.

---

## 🔗 Luồng End-to-End Hoàn Chỉnh

```
┌─────────────────────────────────────────────────────────────────┐
│                    CROSS-MODULE TESTING FLOW                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  📋 Bước 0: Phân tích Requirements từng Module                  │
│      Workflow: $generate-requirements-from-website (chạy N lần) │
│                          ↓                                       │
│  📊 Bước 1: Phân Tích Cross-Module & Sinh Ma Trận              │
│      Workflow: $generate-cross-module-test-plan    ← MỚI        │
│      Output: Data Flow Map + Ma trận kết hợp                    │
│                          ↓                                       │
│  🗃️ Bước 2: Sinh Test Data Cho Ma Trận                         │
│      Workflow: $generate-combinatorial-test-data   ← MỚI        │
│      Output: Bộ test data (offline hoặc trên hệ thống)         │
│                          ↓                                       │
│  📝 Bước 3: Sinh Test Cases Chi Tiết                            │
│      Workflow: $generate-manual-testcases-rbt (FULL RBT)        │
│      Input: Ma trận + Requirements                              │
│      Output: Test cases đầy đủ                                  │
│                          ↓                                       │
│  🤖 Bước 4: Sinh Automation Scripts                             │
│      Workflow: $generate-automation-from-testcases              │
│      Output: Scripts PASS stable                                │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📁 Cấu trúc thư mục

```
plans/cross-module/
├── README.md              ← Giới thiệu + Tổng quan (bạn đang đọc file này)
└── QUICK_START.md         ← Hướng dẫn sử dụng nhanh (prompt mẫu + luồng chạy)
```

**Workflow skills tham chiếu:**

```
.agents/skills/
├── generate-cross-module-test-plan/SKILL.md       ← Phân tích + Ma trận
└── generate-combinatorial-test-data/SKILL.md      ← Sinh test data
```

**Skill mở rộng:**

```
.agents/skills/test-data-generator/SKILL.md   ← Multi-Step Pipeline + Combinatorial Data
```

---

## 📋 Hướng dẫn nhanh

Xem file `QUICK_START.md` trong thư mục này để bắt đầu nhanh.
