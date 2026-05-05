# Архітектура мультиагентної системи

## Агенти

| Role | File | Відповідальність |
| ---- | ---- | --------------- |
| Architect | [`.ai/agents/roles/architect.md`](../agents/roles/architect.md) | Проєктує структуру, протоколи, артефакти |
| Orchestrator | [`.ai/agents/roles/orchestrator.md`](../agents/roles/orchestrator.md) | Координує агентів, підтримує стан |
| Worker | [`.ai/agents/roles/worker.md`](../agents/roles/worker.md) | Виконує конкретні задачі |
| Reviewer | [`.ai/agents/roles/reviewer.md`](../agents/roles/reviewer.md) | Перевіряє якість артефактів |
| Researcher | [`.ai/agents/roles/researcher.md`](../agents/roles/researcher.md) | Досліджує, збирає інформацію |

## Канали комунікації

Агенти не спілкуються напряму — вони взаємодіють через **артефакти в репозиторії**:

- [`.ai/memory/state/project-state.yaml`](../memory/state/project-state.yaml) — канонічний стан проєкту
- [`.ai/logs/sessions/`](../logs/sessions/) — журнал сесій (Handoff Packages)
- [`.ai/memory/decisions/`](../memory/decisions/) — архітектурні рішення (ADR)

## Правила доступу до пам'яті

- **Read**: усі агенти читають [`.ai/memory/`](../memory/) та [`.ai/logs/sessions/`](../logs/sessions/).
- **Write**:
  - [`.ai/memory/state/`](../memory/state/) — тільки Orchestrator (або Architect за його дорученням).
  - [`.ai/memory/decisions/`](../memory/decisions/) — Architect або Orchestrator.
  - [`.ai/logs/sessions/`](../logs/sessions/) — будь-який агент, що завершив сесію.

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
