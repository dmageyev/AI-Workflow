# Task: Create Plan

## Вхідні дані (заповни перед відправкою)

- **Мета:** `<опиши ціль>`
- **Контекст:** `<посилання на project-state.yaml або handoff>`
- **Обмеження:** `<дедлайн, ресурси тощо>`

## Завдання для агента

1. Прочитай `.ai/memory/state/project-state.yaml`.
2. Прочитай останній handoff у `.ai/logs/sessions/`.
3. Сформуй план у вигляді списку work items:
   - `id`: унікальний ідентифікатор (наприклад, `FEAT-001`)
   - `title`: назва задачі
   - `owner`: роль агента
   - `status`: `todo`
   - `acceptance_criteria`: чеклист
4. Запропонуй оновлення `project-state.yaml`.

## Очікуваний результат

- Список work items у форматі YAML.
- Оновлений `project-state.yaml` (або diff).
