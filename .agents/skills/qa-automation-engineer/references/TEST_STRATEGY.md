# Test Strategy

## Hướng Dẫn Sử Dụng

File này định nghĩa chiến lược testing cho dự án. Agent tham khảo file này để hiểu scope, ưu tiên, và approach khi sinh test cases hoặc automation scripts.

> ⚠️ **Bạn cần cập nhật file này** cho mỗi dự án cụ thể. Dưới đây là template.

---

## Testing Objectives

- Đảm bảo chất lượng phần mềm qua các cấp độ test
- Phát hiện lỗi sớm trong development lifecycle
- Duy trì regression suite ổn định cho CI/CD

## Scope of Testing

| Loại Test | Áp dụng | Tool/Framework |
|-----------|---------|----------------|
| UI Functional Testing | ✅ | Selenium / Playwright |
| API Testing | ✅ | REST Assured / Postman |
| Unit Testing | ✅ | JUnit / TestNG |
| Integration Testing | ✅ | TestNG + REST Assured |
| Performance Testing | ⬜ | JMeter / k6 |
| Security Testing | ⬜ | OWASP ZAP |
| Mobile Testing | ⬜ | Appium |

## Test Automation Strategy

### Framework Architecture
- **Design Pattern:** Page Object Model (POM)
- **Language:** Java
- **Test Runner:** TestNG
- **Build Tool:** Maven
- **Reporting:** Allure / ExtentReports

### Automation Scope
- Smoke tests: Bao phủ happy path của các chức năng chính
- Regression tests: Bao phủ tất cả test cases đã pass
- Data-driven tests: Sử dụng external data sources (Excel, CSV, JSON)

## Test Data Management

- Sử dụng random data có prefix + timestamp để traceable
- Tách biệt test data khỏi test logic
- Không hard-code credentials trong code

## Execution Plan

| Phase | Mô tả | Trigger |
|-------|--------|---------|
| Smoke Test | Happy path chính | Mỗi build |
| Regression | Full suite | Trước release |
| Integration | API + UI | Hàng ngày |

## Test Environment

- Test chạy trên môi trường Staging
- CI/CD pipeline chạy headless mode
- Local debug chạy headed mode (viewport 1920x1080)
