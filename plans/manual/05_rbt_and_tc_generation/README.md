# Bước 5: Sinh Test Case chi tiết (RBT & Test Case Generation)


---

## Mục đích

Sinh Test Case chi tiết dựa trên chiến lược **Risk-Based Testing (RBT)**: rủi ro cao → test kỹ, rủi ro thấp → test cơ bản.

## Cách sử dụng

1. Đảm bảo đã review và xác nhận scenarios ở Bước 4.
2. Gửi file `prompt.txt` cho AI, tùy chỉnh phần `[Gợi ý]` nếu cần.
3. AI sẽ sinh test cases đầy đủ: Title, Pre-condition, Steps, Expected Result, Test Data, Risk Level, Priority.
4. Review kết quả → sang Bước 6.

## Mẹo quan trọng

### Chia nhỏ khi nhiều module
Nếu Bước 4 có >5 modules, **đừng bảo AI sinh hết 1 lần**. Thay vào đó:
```
Hãy sinh Test Case cho Module 1 và Module 2 trước tiên.
```
Sau khi review xong, tiếp tục:
```
Tiếp tục sinh Test Case cho Module 3 và Module 4.
```

### Test Data phải cụ thể
AI sẽ sinh test data giả lập sát thực tế thay vì placeholder:
- ✅ `test_customer_01@domain.com` thay vì ❌ `email hợp lệ`
- ✅ `KH-2026-0012` thay vì ❌ `mã số hợp lệ`

### Risk Level quyết định độ sâu
| Risk Level | Số TC dự kiến | Bao phủ |
|------------|--------------|---------|
| **High** | 8-15+ TC/module | Happy + Negative + Boundary + Edge |
| **Medium** | 4-8 TC/module | Happy + Negative chính |
| **Low** | 2-4 TC/module | Happy path cơ bản |

### Kỹ thuật thiết kế Test Case

Prompt đã tích hợp 4 kỹ thuật kinh điển để AI sinh test case có hệ thống:

| Kỹ thuật | Khi nào dùng | Ví dụ |
|----------|-------------|-------|
| **Equivalence Partitioning** | Trường có nhiều loại input | Tuổi: <18, 18-60, >60 |
| **Boundary Value Analysis** | Trường có min/max | Password 6-20 ký tự: test 5,6,20,21 |
| **Decision Table** | Logic nhiều điều kiện kết hợp | Login: email + password + active status |
| **State Transition** | Đối tượng có workflow/trạng thái | Đơn hàng: Mới → Xử lý → Giao → Hoàn thành |
