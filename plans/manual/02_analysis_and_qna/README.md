# Bước 2: Phân tích yêu cầu và Q&A (Requirement Analysis)

---

## Mục đích

Yêu cầu AI phân tích tài liệu từ Bước 1 để tìm ra các điểm thiếu sót, mâu thuẫn, chưa rõ ràng (Ambiguities) **trước khi** viết kịch bản. Bước này mô phỏng tư duy Tester đọc tài liệu và đặt câu hỏi cho BA/PO.

## Cách sử dụng

1. Copy nội dung `prompt.txt` và gửi ngay sau khi AI đã xác nhận ở Bước 1.
2. AI sẽ trả về:
   - Danh sách **luồng** (Happy / Alternate / Exception Paths)
   - Danh sách **Ambiguities** (điểm mờ phát hiện)
   - Danh sách **câu hỏi Q&A** có đánh số
3. **Đọc kỹ** từng câu hỏi và trả lời cho AI.
4. Khi đã giải đáp hết → sang Bước 3.

## ⚠️ Lưu ý quan trọng

- **Đây là bước quan trọng nhất** trong quy trình. Nếu bỏ qua, AI sẽ tự đoán logic → test case sai nghiêm trọng.
- Trả lời **càng cụ thể càng tốt**. Nếu chưa biết, nói rõ "Chưa xác định, giả định là..." để AI ghi nhận.
- Có thể bổ sung thêm gợi ý vào phần `[...]` trong prompt.txt để AI tập trung vào mảng bạn quan tâm.

