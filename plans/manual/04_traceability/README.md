# Bước 4: Đảm bảo độ bao phủ (Traceability & Gap Analysis)


---

## Mục đích

Kiểm tra chéo (Cross-check) và thiết lập **Ma trận truy vết (Traceability Matrix)** để đảm bảo 100% yêu cầu gốc đều được phủ kịch bản kiểm thử (Test Scenarios).

## Cách sử dụng

1. Gửi file `prompt.txt` sau khi đã review kết quả phân rã ở Bước 3.
2. AI sẽ trả về:
   - **Traceability Matrix:** Bảng map REQ ID ↔ Module ↔ Scenario
   - **Gap Analysis:** Báo cáo thiếu sót (nếu có)
   - **High-Level Scenarios:** Danh sách kịch bản cấp cao
3. **Review kỹ** danh sách scenarios:
   - Có scenario nào bị thiếu không?
   - Có scenario nào thừa / trùng lặp không?
   - Bổ sung thêm nếu cần → Xác nhận → sang Bước 5.

## ⚠️ Human Checkpoint

**Đây là điểm chốt chặn nhân sự.** Lý do:

- AI có thể bỏ sót các edge case đặc thù của dự án.
- Tester (con người) cần tự đánh giá **mức độ rủi ro** cho từng module **trước khi** cho AI sinh test case chi tiết ở Bước 5.
- Nếu phát hiện thiếu, yêu cầu AI bổ sung: *"Hãy thêm scenarios cho trường hợp [X]"*.
