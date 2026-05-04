# Changelog

Усі значущі зміни цього шаблону документуються тут.

Формат базується на [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

### Added

- Протокол відновлення після збою сесії в `03-handoff-protocol.md`
- Розділи "Коли НЕ залучати" та "Взаємодія" у всіх role-файлах агентів
- Перша реальна bootstrap-сесія в `.ai/logs/sessions/2026-05-04-2200-bootstrap/`
- `CONTRIBUTING.md` з правилами внеску
- GitHub templates: issue (improvement, bug), PR template, CODEOWNERS
- `CHANGELOG.md` (цей файл)
- Filled examples у task-промптах
- Few-shot examples у системних промптах
- CI-перевірка структури сесій (наявність snapshot.yaml + handoff.md)
- Нові work_items в `project-state.yaml` для відслідковування покращень
- Таблиця різниці між `snapshot.yaml` та `project-state.yaml`

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
