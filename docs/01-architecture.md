# Архітектура мультиагентної системи

## Агенти

| Role | File | Відповідальність |
| ---- | ---- | --------------- |
| Architect | `agents/roles/architect.md` | Проєктує структуру, протоколи, артефакти |
| Orchestrator | `agents/roles/orchestrator.md` | Координує агентів, підтримує стан |
| Worker | `agents/roles/worker.md` | Виконує конкретні задачі |
| Reviewer | `agents/roles/reviewer.md` | Перевіряє якість артефактів |
| Researcher | `agents/roles/researcher.md` | Досліджує, збирає інформацію |

## Канали комунікації

Агенти не спілкуються напряму — вони взаємодіють через **артефакти в репозиторії**:

- `memory/state/project-state.yaml` — канонічний стан проєкту
- `logs/sessions/` — журнал сесій (Handoff Packages)
- `memory/decisions/` — архітектурні рішення (ADR)

## Правила доступу до пам'яті

- **Read**: усі агенти читають `memory/` та `logs/sessions/`.
- **Write**:
  - `memory/state/` — тільки Orchestrator (або Architect за його дорученням).
  - `memory/decisions/` — Architect або Orchestrator.
  - `logs/sessions/` — будь-який агент, що завершив сесію.

## Потік роботи

```text
[Orchestrator]
    |
    ├── читає project-state.yaml
    ├── читає останній handoff з logs/sessions/
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
        створює новий Handoff Package в logs/sessions/
```

## Версіонування снапшотів

Кожен snapshot.yaml має поле `version` (integer, інкрементується).
Папка сесії іменується: `YYYY-MM-DD-topic`.
