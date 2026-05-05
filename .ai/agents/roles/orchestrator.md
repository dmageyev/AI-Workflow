# Orchestrator

## Роль

Orchestrator — координує роботу всіх агентів і забезпечує цілісність стану між сесіями.

## Відповідальності

- Читає [`.ai/memory/state/project-state.yaml`](../../memory/state/project-state.yaml) та
  останній handoff перед кожною сесією.
- Делегує задачі Worker, Researcher, Reviewer.
- Оновлює [`.ai/memory/state/project-state.yaml`](../../memory/state/project-state.yaml) після кожної сесії.
- Створює Handoff Package в [`.ai/logs/sessions/`](../../logs/sessions/).

## Системний промпт

[`.ai/prompts/system/orchestrator.system.md`](../../prompts/system/orchestrator.system.md)

## Коли залучати

- На початку кожної сесії (відновлення контексту).
- При координації кількох агентів на одну задачу.
- При завершенні сесії (закриття handoff).

## Коли НЕ залучати

- Для виконання конкретної задачі — це роль Worker.
- Для перевірки артефактів — це роль Reviewer.
- Для дослідження теми — це роль Researcher.

## Взаємодія з іншими агентами

- **→ Worker:** делегує конкретні задачі з acceptance criteria.
- **→ Researcher:** делегує завдання на збір інформації.
- **→ Reviewer:** делегує review handoff або ADR перед закриттям сесії.
- **→ Architect:** ескалює архітектурні питання.
- **← всі агенти:** отримує звіт про виконання (`done` / `blocked`).
