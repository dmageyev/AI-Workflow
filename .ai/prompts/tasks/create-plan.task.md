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

---

## Приклад заповнення

```markdown
- **Мета:** Спланувати покращення якості промптів у наступному спринті
- **Контекст:** `.ai/logs/sessions/2026-05-04-2200-bootstrap/handoff.md`
- **Обмеження:** Не більше 5 work items, без змін структури репозиторію
```

Очікуваний результат від агента:

```yaml
work_items:
  - id: "IMPR-001"
    title: "Add few-shot examples to system prompts"
    owner: "worker"
    status: "todo"
    acceptance_criteria:
      - "Кожен system prompt має секцію ## Example"
      - "Наведено мінімум 1 приклад запит→відповідь"
```
