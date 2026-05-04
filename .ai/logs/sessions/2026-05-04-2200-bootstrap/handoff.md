# Handoff Package

## Context (UA)

- **Project:** AI-Workflow
- **Date:** 2026-05-04
- **Time (UTC):** 22:00
- **Topic:** bootstrap
- **Session folder:** `.ai/logs/sessions/2026-05-04-2200-bootstrap/`

## Session prompt

**Text:**

> Розгорни повну структуру репозиторію AI-Workflow для мультиагентної роботи.
> Структура має включати: директорії для агентів, промптів, документації, пам'яті,
> workflows та журналу сесій. Усі файли мають відповідати визначеним шаблонам.

**Plan:**

Агент інтерпретував завдання як одноразову bootstrap-сесію: розгорнути усі директорії
та базові файли репозиторію, які слугуватимуть шаблоном для майбутньої мультиагентної
роботи. Жодної реальної бізнес-логіки — лише структура, конвенції та документація.

## Goals

- [x] Розгорнути структуру `.ai/` директорій
- [x] Створити ролі агентів (architect, orchestrator, worker, reviewer, researcher)
- [x] Створити системні промпти для всіх агентів
- [x] Написати документацію (00-vision через 05-agent-requests)
- [x] Налаштувати templates для handoff та snapshot
- [x] Налаштувати CI (markdownlint + yamllint)
- [x] Зафіксувати архітектурне рішення ADR-0001

## What was done

- [x] Створено всю структуру `.ai/` (docs, agents, prompts, memory, workflows, logs)
- [x] Написано 6 документів архітектури (`00-vision.md` → `05-agent-requests.md`)
- [x] Написано 5 ролей агентів та 5 системних промптів
- [x] Написано 4 task-промпти (create-plan, debug, implement-feature, review)
- [x] Написано 2 handoff-шаблони (handoff.template.md, snapshot.template.yaml)
- [x] Написано glossary.uk.md, domain-notes.md, project-state.yaml
- [x] Написано workflows/runbook.uk.md та examples/example-handoff.md
- [x] Налаштовано `.github/workflows/lint.yml` (markdownlint + yamllint)
- [x] Зафіксовано ADR-0001 (запис архітектурних рішень)

## Key decisions

- Decision links: [`memory/decisions/0001-record-architecture.md`](../../memory/decisions/0001-record-architecture.md)

## Current state

- **Snapshot:** [`logs/sessions/2026-05-04-2200-bootstrap/snapshot.yaml`](snapshot.yaml)
- **Open questions:**
  - Яку конкретну задачу буде вирішувати перша реальна сесія після bootstrap?
- **Blockers:**
  - немає

## Next actions (ordered)

1. Визначити першу реальну задачу проєкту та додати її до `project-state.yaml` як `FEAT-001`
2. Запустити Orchestrator для делегування задачі відповідному агенту
3. Переглянути та доповнити `domain-notes.md` специфічними знаннями предметної галузі
4. Розглянути додавання CI-перевірки структури сесій (наявність snapshot.yaml + handoff.md)

## Files changed / created

- `.ai/docs/00-vision.md`
- `.ai/docs/01-architecture.md`
- `.ai/docs/02-workflow.md`
- `.ai/docs/03-handoff-protocol.md`
- `.ai/docs/04-quality-gates.md`
- `.ai/docs/05-agent-requests.md`
- `.ai/agents/registry.yaml`
- `.ai/agents/roles/architect.md`
- `.ai/agents/roles/orchestrator.md`
- `.ai/agents/roles/worker.md`
- `.ai/agents/roles/reviewer.md`
- `.ai/agents/roles/researcher.md`
- `.ai/prompts/system/orchestrator.system.md`
- `.ai/prompts/system/architect.system.md`
- `.ai/prompts/system/agent.worker.system.md`
- `.ai/prompts/system/agent.reviewer.system.md`
- `.ai/prompts/system/agent.researcher.system.md`
- `.ai/prompts/tasks/create-plan.task.md`
- `.ai/prompts/tasks/debug.task.md`
- `.ai/prompts/tasks/implement-feature.task.md`
- `.ai/prompts/tasks/review.task.md`
- `.ai/prompts/handoff/handoff.template.md`
- `.ai/prompts/handoff/snapshot.template.yaml`
- `.ai/memory/state/project-state.yaml`
- `.ai/memory/decisions/0001-record-architecture.md`
- `.ai/memory/knowledge/domain-notes.md`
- `.ai/memory/glossary.uk.md`
- `.ai/workflows/runbook.uk.md`
- `.ai/workflows/examples/example-handoff.md`
- `.ai/logs/sessions/README.md`
- `.github/workflows/lint.yml`
- `README.md`
- `llms.txt`

## Acceptance criteria

- [x] Усі директорії `.ai/` присутні
- [x] Кожен агент має role-файл та системний промпт
- [x] CI проходить (markdownlint + yamllint)
- [x] project-state.yaml містить поточний стан
- [x] Цей handoff package збережено у `.ai/logs/sessions/`
