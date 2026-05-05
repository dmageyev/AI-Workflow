# Project Status

> Оновлюється Orchestrator після кожної сесії.

| Поле | Значення |
| ---- | -------- |
| **Фаза** | `review` |
| **Прогрес** | 90% |
| **Остання сесія** | [`.ai/logs/sessions/2026-05-05-0231-scale-005/`](./logs/sessions/2026-05-05-0231-scale-005/) |
| **Відкритих work items** | 1 |
| **Остання зміна** | 2026-05-05 |

## Як оновлювати

Orchestrator оновлює цей файл наприкінці кожної сесії:

1. Змінити `Фаза` відповідно до `state.phase` у `project-state.yaml`.
2. Змінити `Прогрес` відповідно до `state.progress`.
3. Оновити посилання на `Остання сесія` — шлях до нової папки сесії.
4. Порахувати кількість work items зі статусом `todo` або `in-progress`.
5. Оновити `Остання зміна` — дата поточної сесії.

## Посилання

- Детальний стан: [`project-state.yaml`](./memory/state/project-state.yaml)
- Архів завершених задач: [`work-items-archive.yaml`](./memory/state/work-items-archive.yaml)
- Дорожня карта: [`ROADMAP.md`](./ROADMAP.md)
