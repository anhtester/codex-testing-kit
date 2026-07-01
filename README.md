# Codex Testing Kit 🚀

👋 Chào mừng bạn đến với **Codex Testing Kit** — bộ công cụ kiểm thử phần mềm dành cho **OpenAI Codex**!

Đây là bộ Kit được xây dựng và phát triển bởi **Anh Tester**, dành cho **Cộng đồng Tester Việt Nam**. Repository cung cấp sẵn quy tắc làm việc (Rules), kỹ năng tái sử dụng (Skills), quy trình chuyên sâu (Plans) và prompt mẫu để Codex hỗ trợ hiệu quả cả **Manual Testing** lẫn **Automation Testing**.

Bộ Kit bao phủ quy trình kiểm thử từ phân tích yêu cầu, thiết kế test cases, sinh test data, xây dựng framework, viết automation scripts, kiểm thử API, xử lý flaky tests cho đến tích hợp Jira/Xray.

---

## 🌟 Tính Năng Nổi Bật

- **🔁 Quy trình AI End-to-End:** Phân tích Requirements → thiết kế Test Cases → sinh Test Data → viết Automation Scripts → chạy test → phân tích và sửa lỗi.
- **📋 Manual & Automation Testing:** Hỗ trợ AI-RBT, test plan, traceability, Playwright, Selenium, Appium và API testing.
- **🧠 26 Codex Skills chuyên biệt:** Codex tự chọn skill theo yêu cầu hoặc người dùng gọi trực tiếp bằng cú pháp `$skill-name`.
- **🧭 Quy tắc QA nhất quán:** Áp dụng POM, locator strategy, smart waits, dữ liệu deterministic và delivery checklist.
- **🌐 Khám phá UI thực tế:** Hỗ trợ inspect DOM, sinh locator ổn định và hạn chế việc đoán selector.
- **🛠️ Self-fix Workflow:** Chạy test, đọc lỗi, sửa code và kiểm tra lại bằng lệnh test/lint/compile phù hợp.
- **🇻🇳 Giao tiếp bằng tiếng Việt:** Hướng dẫn và báo cáo được tối ưu cho Tester Việt Nam.

---

## 📂 Cấu Trúc Thư Mục Chính

```text
codex-testing-kit/
├── .agents/
│   ├── rules/              # 6 bộ quy tắc QA và automation
│   └── skills/             # 26 Codex skills/workflows
├── plans/
│   ├── manual/             # Quy trình Manual Testing AI-RBT 6 bước
│   ├── automation/         # Quy trình Automation Testing 6 bước
│   └── cross-module/       # Cross-module và ma trận tổ hợp
├── prompt_templates/       # Prompt mẫu dùng nhanh
├── AGENTS.md               # Chỉ dẫn cấp repository cho Codex
└── README.md
```

### `AGENTS.md` — Chỉ Dẫn Chung Cho Codex

Codex tự đọc `AGENTS.md` trước khi làm việc trong repository. File này quy định:

- Khi nào cần dùng repository skills trong `.agents/skills`.
- Rule nào cần đọc cho Playwright, Selenium, Appium, locator và test data.
- Cách tương thích với các tên tool cũ còn tồn tại trong tài liệu đã migrate.
- Quy ước giao tiếp, bảo toàn trạng thái Git và cách kiểm chứng automation code.

Nếu dự án có thêm `AGENTS.md` hoặc `AGENTS.override.md` trong thư mục con, chỉ dẫn gần thư mục đang làm việc hơn sẽ có độ ưu tiên cao hơn.

### `.agents/skills/` — Codex Skills Và Workflows

Mỗi skill là một thư mục chứa `SKILL.md` với `name`, `description`, hướng dẫn thực thi và tài nguyên liên quan. Codex có thể kích hoạt skill theo hai cách:

1. **Gọi trực tiếp:** Gõ `$` và chọn skill, hoặc viết `$skill-name` trong prompt.
2. **Tự động:** Codex chọn skill khi yêu cầu khớp với phần `description`.

Một số workflow chính:

| Skill | Mục đích |
|-------|----------|
| `$generate-requirements-from-website` | Phân tích website và sinh Requirements |
| `$analyze-requirement-document` | Phân tích Jira ticket, user story hoặc tài liệu yêu cầu |
| `$generate-testcases-from-requirements` | Sinh test cases nhanh — QUICK mode |
| `$generate-manual-testcases-rbt` | Sinh test cases theo AI-RBT đầy đủ |
| `$generate-application-test-plan` | Khám phá ứng dụng và sinh test plan |
| `$generate-automation-framework` | Scaffold framework Playwright, Selenium hoặc Appium |
| `$generate-automation-from-testcases` | Chuyển manual test cases thành automation scripts |
| `$generate-automation-from-ui-flow` | Sinh automation từ UI flow và DOM thực tế |
| `$generate-api-tests-from-swagger` | Sinh API tests từ Swagger/OpenAPI |
| `$generate-locator` | Sinh locator ổn định cho UI element |
| `$generate-test-data` | Sinh test data có cấu trúc và traceable |
| `$analyze-flaky-tests` | Phân tích hoặc khắc phục flaky tests |
| `$generate-cross-module-test-plan` | Sinh module map và ma trận tổ hợp |
| `$generate-combinatorial-test-data` | Sinh dữ liệu cho ma trận cross-module |
| `$fetch-jira-requirements` | Lấy Requirements/User Stories từ Jira |
| `$import-test-results-xray` | Đẩy kết quả automation lên Xray |

Ngoài các workflow trên, repository còn có các skill nền tảng như `$qa-automation-engineer`, `$rbt-manual-testing`, `$requirements-analyzer`, `$framework-architect`, `$ui-debug-agent`, `$smart-locator-agent`, `$locator-healer-agent`, `$test-data-generator`, `$flaky-test-analyzer` và `$jira-integration`.

### `.agents/rules/` — Quy Tắc Bắt Buộc

| File | Phạm vi |
|------|---------|
| `automation_rules.md` | Quy ước automation, POM, naming và test data |
| `locator_strategy.md` | Thứ tự ưu tiên locator ổn định |
| `playwright_rules.md` | Quy tắc riêng cho Playwright |
| `selenium_rules.md` | Quy tắc riêng cho Selenium |
| `appium_rules.md` | Quy tắc riêng cho Appium |
| `delivery_checklist.md` | Checklist kiểm chứng trước khi bàn giao |

Các rule này không phải slash commands. `AGENTS.md` và từng skill sẽ hướng dẫn Codex đọc đúng rule cần thiết cho tác vụ hiện tại.

---

## 🗺️ `plans/` — Quy Trình Chuyên Sâu

Dùng `plans/` khi tác vụ phức tạp và cần thực hiện tuần tự trong cùng một cuộc hội thoại.

| Plan | Mô tả | Bắt đầu nhanh |
|------|-------|---------------|
| `plans/manual/` | Sinh Manual Test Cases theo quy trình **AI-RBT 6 bước** | [`plans/manual/QUICK_START.md`](plans/manual/QUICK_START.md) |
| `plans/automation/` | Sinh Automation Scripts theo quy trình context → review | [`plans/automation/QUICK_START.md`](plans/automation/QUICK_START.md) |
| `plans/cross-module/` | Phân tích nhiều module và sinh ma trận Pairwise/Cartesian | [`plans/cross-module/QUICK_START.md`](plans/cross-module/QUICK_START.md) |

**Cách dùng:** Mở file `QUICK_START.md` phù hợp, cung cấp input và thực hiện tuần tự các checkpoint. Với Codex, ưu tiên gọi skill tương ứng bằng `$kebab-case`.

---

## 📝 `prompt_templates/` — Prompt Mẫu Dùng Nhanh

Dùng cho tác vụ đơn lẻ: mở prompt → thay nội dung trong `[...]` → paste vào Codex → gửi.

| # | Prompt | Codex skill |
|---|--------|-------------|
| 01 | `prompt_01_generate_requirements.txt` | `$generate-requirements-from-website` |
| 02 | `prompt_02_generate_test_cases.txt` | `$generate-testcases-from-requirements` |
| 03 | `prompt_03_create_framework_playwright.txt` | `$generate-automation-framework` |
| 03 | `prompt_03_create_framework_selenium.txt` | `$generate-automation-framework` |
| 04 | `prompt_04_generate_script_playwright.txt` | `$generate-automation-from-testcases` |
| 04 | `prompt_04_generate_script_selenium.txt` | `$generate-automation-from-testcases` |
| 05 | `prompt_05_convert_manual_to_automation.txt` | `$generate-automation-from-testcases` |
| 07 | `prompt_07_generate_test_data.txt` | `$generate-test-data` |
| 08 | `prompt_08_analyze_flaky_tests.txt` | `$analyze-flaky-tests` |
| 09 | `prompt_09_generate_api_tests.txt` | `$generate-api-tests-from-swagger` |

> Các prompt đã dùng sẵn cú pháp Codex `$kebab-case`. Hãy giữ nguyên dòng gọi skill ở đầu file khi copy prompt vào Codex.

---

## ✳️ Hướng Dẫn Sử Dụng Với Codex

### Cách 1: Codex App

1. Clone repository này hoặc copy `.agents/`, `AGENTS.md`, `plans/` và `prompt_templates/` vào thư mục gốc của dự án cần test.
2. Mở **Codex App** và chọn thư mục dự án.
3. Tạo thread ở chế độ **Local**.
4. Gọi skill trực tiếp trong prompt, ví dụ:

   ```text
   $generate-manual-testcases-rbt

   Hãy sinh test cases cho requirement trong file requirements/login.md.
   ```

Codex sẽ đọc `AGENTS.md`, tải `SKILL.md` liên quan và thực hiện workflow.

### Cách 2: Codex CLI

1. Mở terminal tại thư mục dự án đã chứa `.agents/` và `AGENTS.md`.
2. Khởi chạy Codex:

   ```bash
   codex
   ```

3. Gõ `$` để chọn skill hoặc dùng `/skills` để xem danh sách skills.
4. Gửi yêu cầu kèm skill cần dùng:

   ```text
   $generate-automation-from-testcases

   Chuyển các test cases trong testcases/login.md thành Playwright TypeScript.
   ```

### Cách 3: Codex IDE Extension

1. Cài Codex extension cho VS Code hoặc IDE được hỗ trợ.
2. Mở dự án đã chứa `.agents/` và `AGENTS.md`.
3. Đăng nhập bằng tài khoản ChatGPT hoặc OpenAI API key.
4. Mở Codex panel và gọi skill bằng `$skill-name` như trong Codex App/CLI.

### Cách 4: Để Codex Tự Chọn Skill

Không bắt buộc phải nhớ tên skill. Bạn có thể mô tả mục tiêu bằng ngôn ngữ tự nhiên:

```text
Phân tích file Swagger này, sinh test cases API và automation scripts bằng Playwright API.
```

Codex sẽ đối chiếu yêu cầu với `description` của các skills để chọn workflow phù hợp. Khi cần kiểm soát chính xác workflow, nên gọi skill trực tiếp bằng `$skill-name`.

---

## 🔄 Mapping Từ Cú Pháp Cũ Sang Codex

| Thành phần | Cú pháp cũ | Codex |
|------------|------------|-------|
| Chỉ dẫn repository | `GEMINI.md` hoặc `CLAUDE.md` | `AGENTS.md` |
| Workflow | `.agent/workflows/*.md` hoặc `.claude/commands/*.md` | `.agents/skills/<skill-name>/SKILL.md` |
| Quy tắc QA | `.agent/rules/` | `.agents/rules/` |
| Gọi workflow | `/generate_automation_from_testcases` | `$generate-automation-from-testcases` |
| Naming | `snake_case` | `kebab-case` |

Ví dụ mapping đầy đủ:

```text
/generate_manual_testcases_rbt
→ $generate-manual-testcases-rbt
→ .agents/skills/generate-manual-testcases-rbt/SKILL.md
```

Codex không cần một thư mục `commands/` riêng cho các workflow của Kit này; mỗi workflow được đóng gói trực tiếp dưới dạng repository skill.

---

## ✅ Gợi Ý Workflow

### Manual Testing

```text
$generate-requirements-from-website
→ $generate-manual-testcases-rbt
→ $generate-test-data
```

### Automation Testing

```text
$generate-automation-framework
→ $generate-automation-from-testcases
→ $analyze-flaky-tests (khi cần)
```

### Cross-Module Testing

```text
$generate-cross-module-test-plan
→ $generate-combinatorial-test-data
→ $generate-manual-testcases-rbt
→ $generate-automation-from-testcases
```

### Jira/Xray

```text
$fetch-jira-requirements
→ thực thi workflow testing phù hợp
→ $import-test-results-xray
```

---

## 📚 Tài Liệu Codex Chính Thức

- [Agent Skills](https://developers.openai.com/codex/skills)
- [Custom instructions với AGENTS.md](https://developers.openai.com/codex/guides/agents-md)
- [Codex App](https://developers.openai.com/codex/app)
- [Codex CLI](https://developers.openai.com/codex/cli)
- [Codex IDE Extension](https://developers.openai.com/codex/ide)

---

## 🤝 Hỗ Trợ & Đóng Góp

- Nếu gặp khó khăn hoặc muốn đóng góp, hãy tạo **Issue** hoặc **Pull Request**.
- Tham gia cộng đồng **Anh Tester** để trao đổi về Manual Testing và Automation Testing:
  - 📘 **Fanpage Facebook:** [Anh Tester](https://www.facebook.com/anhtester)
  - 👥 **Group Facebook Automation:** [Cộng đồng Automation Testing](https://www.facebook.com/groups/automationtest)
  - 👥 **Group Facebook Manual:** [Cộng đồng Manual Testing](https://www.facebook.com/groups/manualtest)
  - ✈️ **Telegram Automation:** [Cộng đồng Automation Testing](https://t.me/+kSUGJ3pVvxkyZWU1)
  - ✈️ **Telegram Manual:** [Cộng đồng Manual Testing](https://t.me/+8eChRz7OVqliZWRl)

---

## 📄 License

Dự án được phân phối theo giấy phép nguồn mở **[MIT License](LICENSE)**.

---

**Anh Tester Automation Testing 🎯**

[https://anhtester.com](https://anhtester.com)
