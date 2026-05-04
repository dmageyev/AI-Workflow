# Workflow: операційна модель

## Цикл сесії

Кожна робоча сесія складається з чотирьох кроків:

### 1. Відновлення контексту (Context Restore)

- Orchestrator читає [`memory/state/project-state.yaml`](../memory/state/project-state.yaml).
- Orchestrator читає останній handoff у [`logs/sessions/`](../logs/sessions/) (сортування за назвою папки).
- Якщо є open questions або blockers — вирішити перед продовженням.

### 2. Планування (Planning)

- Обрати work items зі статусом `todo` або `in-progress`.
- Розподілити задачі між агентами.
- Зафіксувати план у handoff.md поточної сесії (секція "Next actions").

### 3. Виконання (Execution)

- Кожен агент виконує свої задачі та створює артефакти.
- Reviewer перевіряє ключові артефакти.
- Усі нові рішення фіксуються ADR у [`memory/decisions/`](../memory/decisions/).

### 4. Завершення сесії (Session Close)

- Оновити статуси work items у [`memory/state/project-state.yaml`](../memory/state/project-state.yaml).
- Створити Handoff Package:
  - [`logs/sessions/`](../logs/sessions/)`YYYY-MM-DD-HHmm-topic/snapshot.yaml`
  - [`logs/sessions/`](../logs/sessions/)`YYYY-MM-DD-HHmm-topic/handoff.md`
- Перевірити quality gates ([`docs/04-quality-gates.md`](04-quality-gates.md)).
- Закомітити всі зміни.

## Правила іменування папок сесій

Формат: `YYYY-MM-DD-HHmm-kebab-case-topic`

`HHmm` — години та хвилини старту сесії (UTC). Дозволяє мати кілька сесій в один день без колізій.

Приклади:

- `2026-05-04-1430-bootstrap`
- `2026-05-10-0900-implement-feature-auth`
- `2026-05-15-1615-review-architecture`
