# Bước 3: Phân rã hệ thống (Decomposition Strategy)


---

## Mục đích

Hướng dẫn AI chia nhỏ hệ thống / tính năng phức tạp thành nhiều **Module** hoặc **Sub-module** dễ quản lý. Tránh tình trạng AI bị "ngợp" thông tin → viết test case thiếu sót.

## Cách sử dụng

1. Đảm bảo các câu hỏi ở Bước 2 đã được trả lời đầy đủ.
2. Gửi file `prompt.txt` cho AI.
3. AI sẽ trả về:
   - Danh sách **Modules / Sub-modules** với mô tả chức năng
   - **Dependencies** (mối quan hệ phụ thuộc giữa các module)
4. Review nhanh kết quả → sang Bước 4.

## Chiến lược phân rã

Có 3 cách phân rã, tùy theo dự án:

| Cách | Phù hợp khi | Ví dụ |
|------|-------------|-------|
| **Theo UI** | Trang có nhiều section rõ ràng | Header, Sidebar, Data Table, Form Popup |
| **Theo luồng** | Tính năng có nhiều CRUD operations | Flow Tạo mới, Flow Chỉnh sửa, Flow Xóa |
| **Theo đối tượng** | Hệ thống có nhiều entity | Quản lý User, Quản lý Product, Quản lý Order |

Tùy chỉnh phần `[Gợi ý]` trong prompt.txt để AI phân rã theo cách phù hợp nhất.
