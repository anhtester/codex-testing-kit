# Codex Prompt Templates

Thư mục này chứa các prompt mẫu đã tích hợp sẵn lệnh gọi **Codex skill**.

Khi paste prompt vào Codex App, CLI hoặc IDE Extension, Codex sẽ nhận diện skill ở dòng đầu tiên, đọc file `SKILL.md` tương ứng trong `.agents/skills/` và thực hiện đúng workflow.

---

## Danh Sách Prompt

| # | File | Codex workflow skill | Skill nền tảng |
|---|------|----------------------|----------------|
| 01 | `prompt_01_generate_requirements.txt` | `$generate-requirements-from-website` | `$requirements-analyzer` |
| 02 | `prompt_02_generate_test_cases.txt` | `$generate-testcases-from-requirements` | `$rbt-manual-testing` |
| 03 | `prompt_03_create_framework_playwright.txt` | `$generate-automation-framework` | `$framework-architect` |
| 03 | `prompt_03_create_framework_selenium.txt` | `$generate-automation-framework` | `$framework-architect` |
| 04 | `prompt_04_generate_script_playwright.txt` | `$generate-automation-from-testcases` | `$qa-automation-engineer` |
| 04 | `prompt_04_generate_script_selenium.txt` | `$generate-automation-from-testcases` | `$qa-automation-engineer` |
| 05 | `prompt_05_convert_manual_to_automation.txt` | `$generate-automation-from-testcases` | `$qa-automation-engineer` |
| 07 | `prompt_07_generate_test_data.txt` | `$generate-test-data` | `$test-data-generator` |
| 08 | `prompt_08_analyze_flaky_tests.txt` | `$analyze-flaky-tests` | `$flaky-test-analyzer` |
| 09 | `prompt_09_generate_api_tests.txt` | `$generate-api-tests-from-swagger` | `$qa-automation-engineer` |

> Prompt 02 mặc định dùng **QUICK mode** qua `$generate-testcases-from-requirements`. Muốn chạy quy trình AI-RBT 6 bước đầy đủ, đổi dòng đầu thành `$generate-manual-testcases-rbt`.

## Cách Sử Dụng

1. Chọn file prompt phù hợp.
2. Thay các placeholder `[...]` bằng dữ liệu thực tế.
3. Giữ nguyên dòng `$skill-name` ở đầu file.
4. Copy toàn bộ nội dung và paste vào Codex.
5. Kiểm tra các checkpoint hoặc câu hỏi làm rõ do skill yêu cầu.

## Quy Ước Tên

- Codex skill được gọi bằng dấu `$`.
- Tên skill dùng **kebab-case**, ví dụ `$generate-automation-from-testcases`.
- Skill vật lý nằm tại `.agents/skills/<skill-name>/SKILL.md`.
- Không dùng slash command dạng cũ `/generate_automation_from_testcases`.
