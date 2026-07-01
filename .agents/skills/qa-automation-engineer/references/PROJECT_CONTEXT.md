# Project Context

## Hướng Dẫn Sử Dụng

File này chứa thông tin ngữ cảnh của dự án đang test. **Agent cần đọc file này trước khi bắt đầu bất kỳ tác vụ automation nào** để hiểu đúng domain và tech stack.

> ⚠️ **Bạn cần cập nhật file này** cho mỗi dự án cụ thể. Dưới đây là template.

---

## Application Overview

- **Tên ứng dụng:** [Tên app]
- **Mô tả:** [Mô tả ngắn về ứng dụng]
- **Loại:** [Web App / Mobile App / API]
- **URL môi trường test:** [URL staging/test]

## Tech Stack

- **Frontend:** [React / Angular / Vue / ...]
- **Backend:** [Java Spring / Node.js / .NET / ...]
- **Database:** [MySQL / PostgreSQL / MongoDB / ...]
- **Authentication:** [JWT / OAuth2 / Session-based / ...]

## Key Features & Modules

| Module | Mô tả | Priority |
|--------|--------|----------|
| Login | Đăng nhập, quên mật khẩu, 2FA | High |
| Dashboard | Trang tổng quan | Medium |
| User Management | CRUD users, phân quyền | High |
| ... | ... | ... |

## Environment Details

| Môi trường | URL | Credentials |
|------------|-----|-------------|
| Dev | ... | ... |
| Staging | ... | ... |
| Production | ... | N/A (không test trên prod) |

## Notes

- Thêm các lưu ý đặc biệt về business rules, edge cases, hoặc known issues ở đây.
