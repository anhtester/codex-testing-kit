# 📋 Hướng Dẫn Nhanh: Sử Dụng AI-RBT 6 Bước

## 🔀 Chọn Luồng Sử Dụng

Có **2 luồng** riêng biệt, tuỳ tool AI bạn đang dùng:

### Luồng 1: Antigravity (Slash Command) — Tự động

```
Gõ: $generate-manual-testcases-rbt + dán requirements
→ AI tự chạy 6 bước theo skill, dừng ở checkpoint chờ bạn
→ KHÔNG cần copy-paste prompt templates
```

**Ưu điểm:** Nhanh, tự động, agent nhớ context xuyên suốt.
**Nhược điểm:** Hướng dẫn ở mức tổng quát (không chi tiết bằng prompt templates).

### Luồng 2: Copy-Paste Prompt — Thủ công (ChatGPT / Claude / AI bất kỳ)

```
Copy prompt Bước 1 → paste vào chat → AI xử lý
→ Copy prompt Bước 2 → paste → AI xử lý
→ ... lặp lại đến Bước 6
```

**Ưu điểm:** Prompt chi tiết hơn, có ví dụ cụ thể, gợi ý sâu hơn.
**Nhược điểm:** Phải copy-paste thủ công 6 lần.

---

## Luồng 1: Antigravity — Prompt nhanh

```
$generate-manual-testcases-rbt

Dự án: [Tên dự án]
Tính năng: [Tên tính năng]
Mục tiêu: [Mô tả ngắn]

[Dán requirements/user stories vào đây]
```

Khi AI dừng ở checkpoint, chỉ cần trả lời câu hỏi hoặc gõ:
```
Tiếp tục sang Bước [X]
```

---

## Luồng 2: Copy-Paste — Hướng dẫn từng bước

| Bước | Tên | Prompt file | Chờ User? |
|------|-----|-------------|-----------|
| **1** | Context & Role-play | Copy `plans/manual/01_context_and_roleplay/prompt.txt` + điền `[...]` | ✅ Chờ xác nhận |
| **2** | Analysis & QnA | Copy `plans/manual/02_analysis_and_qna/prompt.txt` | ✅ **Chờ trả lời Q&A** |
| **3** | Decomposition | Copy `plans/manual/03_decomposition/prompt.txt` | Review nhanh |
| **4** | Traceability | Copy `plans/manual/04_traceability/prompt.txt` | ✅ **Chờ review scenarios** |
| **5** | RBT & TC Generation | Copy `plans/manual/05_rbt_and_tc_generation/prompt.txt` | Review kết quả |
| **6** | Template Mapping | Copy `plans/manual/06_template_mapping/prompt.txt` | Copy bảng → Excel |

### Sơ đồ luồng:

```
[Bước 1] Copy prompt + dán tài liệu requirements
    ↓  AI xác nhận hiểu → User xác nhận OK
[Bước 2] Copy prompt phân tích
    ↓  AI đặt câu hỏi → ⏸️ User trả lời từng câu
[Bước 3] Copy prompt phân rã
    ↓  AI sinh Module list → User review nhanh
[Bước 4] Copy prompt traceability
    ↓  AI sinh scenarios → ⏸️ User review + bổ sung
[Bước 5] Copy prompt sinh TC
    ↓  AI sinh test cases chi tiết → User review
[Bước 6] Copy prompt chuẩn hóa
    ↓  AI sinh bảng Markdown → Copy vào Excel/Jira ✅
```

---

## Mẹo Tối Ưu

1. **Bước 2 là quan trọng nhất** — Đừng vội, trả lời kỹ từng câu hỏi AI đặt ra
2. **Chia module khi nhiều** — Ở Bước 5, nếu có >5 modules, yêu cầu AI sinh từng module
3. **Review trước khi format** — Ở Bước 5, review test cases trước khi sang Bước 6
4. **Dùng cùng conversation** — Chạy tất cả 6 bước trong **cùng 1 conversation** để AI giữ context
5. **Luồng Copy-Paste chi tiết hơn** — Nếu cần chất lượng cao nhất, dùng Luồng 2 (kể cả khi đang dùng Antigravity)
