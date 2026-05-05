# Changelog

Усі значущі зміни цього шаблону документуються тут.

Формат базується на [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

---

## [1.2.0] — 2026-05-05

### Added in 1.2.0

- Anti-patterns та Edge cases секції у всіх 5 системних промптах
- `delegate.task.md` — шаблон явного делегування задачі від Orchestrator
- `research.task.md` — шаблон запиту до Researcher
- `STATUS.md` — живий дашборд стану проєкту
- `ROADMAP.md` — дорожня карта milestone
- `QUICKSTART.md` — покрокова інструкція для нового агента/людини
- `VERSION` файл із semver версією шаблону
- `.ai/memory/knowledge/README.md` — структура та схема іменування knowledge-файлів
- Секція `## Assumptions` у `handoff.template.md`
- Пріоритети `[HIGH]/[MEDIUM]` у Next actions `handoff.template.md`
- Поле `confidence` у `snapshot.template.yaml`
- Поле `template_version` у `snapshot.template.yaml`
- CI: перевірка мертвих внутрішніх посилань у Markdown (`dead-links-check`)
- CI: перевірка унікальності номерів ADR (`adr-uniqueness-check`)
- CI: перевірка дублікатів ID між `work_items` і архівом (`work-items-id-dedup-check`)
- CI: перевірка синхронності `VERSION` та `CHANGELOG.md` (`version-changelog-sync`)
- Поля `capabilities`, `max_context_items`, `status` у `registry.yaml`
- Секція "Робота в команді" у `06-adapting-template.md`

---

## [1.1.0] — 2026-05-04

### Added in 1.1.0

- Протокол відновлення після збою сесії в `03-handoff-protocol.md`
- Розділи "Коли НЕ залучати" та "Взаємодія" у всіх role-файлах агентів
- Перша реальна bootstrap-сесія в `.ai/logs/sessions/2026-05-04-2200-bootstrap/`
- `CONTRIBUTING.md` з правилами внеску
- GitHub templates: issue (improvement, bug), PR template, CODEOWNERS
- Filled examples у task-промптах
- Few-shot examples у системних промптах
- CI-перевірка структури сесій (наявність snapshot.yaml + handoff.md)
- Нові work_items в `project-state.yaml` для відслідковування покращень
- Таблиця різниці між `snapshot.yaml` та `project-state.yaml`
- Окремий файл `work-items-archive.yaml` для завершених задач

---

## [1.0.0] — 2026-05-04

### Added in 1.0.0

- Повна структура `.ai/` директорій
- 5 ролей агентів: orchestrator, architect, worker, reviewer, researcher
- 5 системних промптів
- 4 task-промпти: create-plan, debug, implement-feature, review
- 6 документів архітектури: 00-vision → 05-agent-requests
- Handoff шаблони: `handoff.template.md`, `snapshot.template.yaml`
- `project-state.yaml`, `glossary.uk.md`, `domain-notes.md`
- `workflows/runbook.uk.md` та `workflows/examples/example-handoff.md`
- CI: markdownlint + yamllint через GitHub Actions
- ADR-0001: запис архітектурних рішень
