# Bước 1: Khởi tạo ngữ cảnh (Context & Role-play)

---

## Mục đích

Thiết lập vai trò **Senior QA Engineer** và nạp bối cảnh dự án để AI định hình tư duy chuyên gia kiểm thử. Bước này giới hạn không gian kiến thức của AI, giúp câu trả lời chuyên sâu và sát thực tế hơn.

## Cách sử dụng

1. Mở file `prompt.txt` trong thư mục này.
2. Copy nội dung bên dưới dòng `---START---`.
3. Thay thế các phần trong `[...]` bằng dữ liệu thực tế:
   - **Tên dự án / tính năng** cần test
   - **Bối cảnh hệ thống** (mô tả ngắn về app hiện tại)
   - **Mục tiêu MVP** (phạm vi kiểm thử đợt này)
   - **Tài liệu đính kèm** (Requirements, User Stories, Figma, PDF...)
4. Paste vào AI chat và gửi.
5. Chờ AI xác nhận **"Tôi đã hiểu bối cảnh và sẵn sàng"** rồi mới sang Bước 2.

## Lưu ý

- Tài liệu càng chi tiết → AI phân tích càng chính xác.
- Nếu có Figma hoặc screenshot, mô tả bổ sung các element UI quan trọng.
- Bước này chỉ cần chạy **1 lần** duy nhất đầu conversation.

