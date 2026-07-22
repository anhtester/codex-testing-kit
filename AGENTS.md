# Codex workspace guidance

## QA automation resources

- Use repository skills from `.agents/skills` when the request matches their `description` or when the user invokes a skill with `$skill-name`.
- Read only the relevant rule files before implementing or reviewing automation code:
  - `.agents/rules/automation_rules.md` for shared automation and test-data conventions.
  - `.agents/rules/api_rules.md` for API automation and OWASP security rules.
  - `.agents/rules/locator_strategy.md` for locator selection.
  - `.agents/rules/playwright_rules.md` for Playwright work.
  - `.agents/rules/selenium_rules.md` for Selenium work.
  - `.agents/rules/appium_rules.md` for Appium work.
  - `.agents/rules/delivery_checklist.md` before completing automation work.
- Invoke workflow skills with `$` and kebab-case, for example `$generate-locator` or `$analyze-flaky-tests`.

## Legacy tool-name compatibility

- Interpret tool names retained in migrated instructions by intent and use the callable Codex equivalent in the current session.
- Map `view_file` to a read-only filesystem command, `write_to_file`/`replace_file_content` to `apply_patch`, and `run_command`/`command_status` to shell execution and its wait mechanism.
- Map `read_url_content` to the available web or in-app browser capability.
- Map conceptual `browser_*` steps to the installed in-app browser skill and its current callable tools; do not invent unavailable tool calls.

## Working expectations

- Communicate and report results in concise, clear Vietnamese.
- Preserve the current local code state. Do not run state-changing Git commands such as `git pull`, `git checkout`, `git merge`, `git rebase`, or `git reset` unless the user explicitly requests them. Read-only Git inspection is allowed.
- Prefer stable semantic locators and smart waits; do not introduce fixed sleeps unless the user explicitly requires them.
- Keep test data unique, traceable, deterministic when seeded, and free of real personal information.
- Validate generated automation with the narrowest relevant test, lint, or compile command available in the target project.
