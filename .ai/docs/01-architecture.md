# Архітектура мультиагентної системи

## Агенти

| Role | File | Відповідальність |
| ---- | ---- | --------------- |
| Architect | [`agents/roles/architect.md`](../agents/roles/architect.md) | Проєктує структуру, протоколи, артефакти |
| Orchestrator | [`agents/roles/orchestrator.md`](../agents/roles/orchestrator.md) | Координує агентів, підтримує стан |
| Worker | [`agents/roles/worker.md`](../agents/roles/worker.md) | Виконує конкретні задачі |
| Reviewer | [`agents/roles/reviewer.md`](../agents/roles/reviewer.md) | Перевіряє якість артефактів |
| Researcher | [`agents/roles/researcher.md`](../agents/roles/researcher.md) | Досліджує, збирає інформацію |

## Канали комунікації

Агенти не спілкуються напряму — вони взаємодіють через **артефакти в репозиторії**:

- [`memory/state/project-state.yaml`](../memory/state/project-state.yaml) — канонічний стан проєкту
- [`logs/sessions/`](../logs/sessions/) — журнал сесій (Handoff Packages)
- [`memory/decisions/`](../memory/decisions/) — архітектурні рішення (ADR)

## Правила доступу до пам'яті

- **Read**: усі агенти читають [`memory/`](../memory/) та [`logs/sessions/`](../logs/sessions/).
- **Write**:
  - [`memory/state/`](../memory/state/) — тільки Orchestrator (або Architect за його дорученням).
  - [`memory/decisions/`](../memory/decisions/) — Architect або Orchestrator.
  - [`logs/sessions/`](../logs/sessions/) — будь-який агент, що завершив сесію.

## Потік роботи

```text
[Orchestrator]
    |
    ├── читає project-state.yaml
    ├── читає останній handoff з .ai/logs/sessions/
    |
    ├── делегує → [Worker / Researcher]
    |                 |
    |                 └── виконує задачу → артефакти
    |
    ├── делегує → [Reviewer]
    |                 |
    |                 └── перевіряє артефакти → approval / rejection
    |
    └── оновлює project-state.yaml
        створює новий Handoff Package в .ai/logs/sessions/
```

## Версіонування снапшотів

Кожен snapshot.yaml має поле `version` (integer, інкрементується).
Папка сесії іменується: `YYYY-MM-DD-HHmm-topic`.
