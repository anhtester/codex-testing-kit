# Bước 6: Chuẩn hóa Format (Template Mapping)


---

## Mục đích

Đóng gói toàn bộ Test Cases đã sinh ở Bước 5 sang bảng Markdown chuẩn, sẵn sàng copy sang **Excel**, **Google Sheets**, hoặc import thẳng lên **Jira/TestRail/Xray/Zephyr**.

## Cách sử dụng

1. Gửi file `prompt.txt` sau khi đã review test cases ở Bước 5.
2. AI sẽ xuất bảng Markdown với format:
   ```
   | TC ID | Module | Risk Level | Test Title | Pre-Condition | Test Steps | Expected Result | Priority | Test Data |
   ```
3. Copy kết quả bảng → paste vào công cụ quản lý test.

## Quy tắc TC ID

Format mặc định: `[DỰ_ÁN]_[MODULE]_TC_[SỐ]`

Ví dụ: `CRM_CUST_TC_001`, `CRM_LOGIN_TC_001`

Nếu dự án có quy ước ID riêng, thay đổi trong phần `[Tùy chỉnh]` của prompt.txt.

## Xử lý khi quá dài

Nếu tổng số Test Cases > 30, AI sẽ tự chia thành **Part 1, Part 2...** và hỏi bạn trước khi tiếp tục. Đảm bảo:
- Không bỏ sót TC nào giữa các phần
- Số thứ tự TC ID liên tục giữa các phần
