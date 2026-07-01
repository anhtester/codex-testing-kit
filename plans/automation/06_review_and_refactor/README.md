# Bước 6: Kiểm duyệt & Tối ưu (Review & Refactoring)

**Workflow:** `$generate-automation-from-testcases` (tiếp tục)
**Skill:** `$qa-automation-engineer`

---

## Mục đích

Sau khi test chạy PASS, "dọn dẹp" code để đạt chuẩn **Clean Code** trước khi merge vào repository. Tránh code rác làm bẩn project.

## Cách sử dụng

1. Gửi file `prompt.txt` sau khi test đã PASS ở Bước 5.
2. AI sẽ thực hiện:
   - Xóa debug logs, commented code, unused variables
   - Review code quality
   - Gắn CI/CD tags (smoke, regression...)
3. Nhận code final → commit/merge.

## Checklist Review

| # | Kiểm tra | Trạng thái |
|---|---|---|
| 1 | Không còn `console.log` / `System.out.println` | ☐ |
| 2 | Không còn commented code | ☐ |
| 3 | Không có unused variables/locators | ☐ |
| 4 | Không có hard sleep | ☐ |
| 5 | Assertions đầy đủ và chính xác | ☐ |
| 6 | Test data unique, traceable | ☐ |
| 7 | Mỗi test case độc lập | ☐ |
| 8 | CI/CD tags đã gắn | ☐ |

## Lưu ý

- Bước này có thể chạy tự động trong workflow One-Click (AI tự cleanup sau khi test PASS).
- Nếu chạy thủ công, paste source code vào để AI review.
- Code phải đạt tiêu chuẩn `.agents/rules/automation_rules.md` trước khi commit.
