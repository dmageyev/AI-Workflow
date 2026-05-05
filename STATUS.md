# Project Status

> Оновлюється Orchestrator після кожної сесії.

| Поле | Значення |
| ---- | -------- |
| **Фаза** | `done` |
| **Прогрес** | 100% |
| **Остання сесія** | `.ai/logs/sessions/2026-05-05-0055-complete/` |
| **Відкритих work items** | 0 |
| **Остання зміна** | 2026-05-05 |

## Як оновлювати

Orchestrator оновлює цей файл наприкінці кожної сесії:

1. Змінити `Фаза` відповідно до `state.phase` у `project-state.yaml`.
2. Змінити `Прогрес` відповідно до `state.progress`.
3. Оновити посилання на `Остання сесія` — шлях до нової папки сесії.
4. Порахувати кількість work items зі статусом `todo` або `in-progress`.
5. Оновити `Остання зміна` — дата поточної сесії.

## Посилання

- Детальний стан: [`.ai/memory/state/project-state.yaml`](./.ai/memory/state/project-state.yaml)
- Архів завершених задач: [`.ai/memory/state/work-items-archive.yaml`](./.ai/memory/state/work-items-archive.yaml)
- Дорожня карта: [`ROADMAP.md`](./ROADMAP.md)
