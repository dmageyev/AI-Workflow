# Roadmap

> Дорожня карта `AI-Workflow` — планові milestone та їх work items.
> Оновлюється Architect або Orchestrator при плануванні нового milestone.

## Як читати

- **Milestone** — логічна група задач, що вирішують одну мету.
- **Status:** `planned` / `in-progress` / `done`
- Work items з milestone можна посилатись на це як `milestone: "v2-improvements"`.

---

## ✅ v1.0 — Bootstrap

**Status:** done | **Закрито:** 2026-05-04

Ціль: розгорнути базову структуру репозиторію-шаблону.

| ID | Назва | Status |
| --- | --- | --- |
| BOOT-001 | Структура `.ai/` директорій | done |
| BOOT-002 | 5 ролей агентів та системні промпти | done |
| BOOT-003 | Handoff шаблони | done |
| BOOT-004 | CI: markdownlint + yamllint | done |
| BOOT-005 | ADR-0001: запис рішень | done |

---

## ✅ v1.1 — Improvements batch 1

**Status:** done | **Закрито:** 2026-05-04

Ціль: підвищити якість промптів та CI-перевірок.

| ID | Назва | Status |
| --- | --- | --- |
| IMPR-001..028 | Few-shot examples, CI checks, GitHub templates | done |
| IMPR-029 | Окремий файл work-items-archive.yaml | done |

---

## ✅ v1.2 — Improvements batch 2

**Status:** done | **Закрито:** 2026-05-05

Ціль: покращення якості передачі контексту, CI та онбордингу.

| ID | Назва | Status |
| --- | --- | --- |
| IMPR-030 | Anti-patterns + Edge cases у системних промптах | done |
| IMPR-031 | delegate.task.md + research.task.md | done |
| IMPR-032 | STATUS.md + ROADMAP.md | done |
| IMPR-033 | knowledge/README.md | done |
| IMPR-034 | Assumptions + confidence у handoff/snapshot шаблонах | done |
| IMPR-035 | CI: dead links + ADR uniqueness + work items dedup | done |
| IMPR-036 | capabilities + status у registry.yaml | done |
| IMPR-037 | QUICKSTART.md | done |
| IMPR-038 | VERSION файл + template_version | done |
| IMPR-039 | Team scale guidance у 06-adapting-template.md | done |

---

## 🔮 v2.0 — Scale & Automation (planned)

**Status:** planned

Ціль: підтримка командної роботи та автоматизація частини workflow.

| ID | Назва | Status |
| --- | --- | --- |
| SCALE-001 | Автогенерація STATUS.md через GitHub Action | planned |
| SCALE-002 | Шаблон multi-owner CODEOWNERS для команд | planned |
| SCALE-003 | Versioned system prompts (теґи git) | planned |
| SCALE-004 | Інтеграційний тест: повний цикл сесії | planned |
