# Як робити запити до агентів

Цей документ описує **структуру та текст промпту** для запитів до агентів в AI-Workflow.

## Загальна структура запиту до агента

Кожен запит до агента складається з трьох частин:

```text
[SYSTEM PROMPT]   ← хто агент, його роль і правила
[CONTEXT]         ← поточний стан, посилання на файли в репо
[TASK]            ← що конкретно потрібно зробити
```

### 1. System prompt (завантажується один раз на початку сесії)

Обери системний промпт з `prompts/system/` відповідно до ролі агента.

| Агент | Файл системного промпту |
| ----- | ----------------------- |
| Architect | `.ai/prompts/system/architect.system.md` |
| Orchestrator | `.ai/prompts/system/orchestrator.system.md` |
| Worker | `.ai/prompts/system/agent.worker.system.md` |
| Reviewer | `.ai/prompts/system/agent.reviewer.system.md` |
| Researcher | `.ai/prompts/system/agent.researcher.system.md` |

### 2. Context (контекст — для кожного запиту)

Перед задачею надай агенту актуальний контекст:

```text
Поточний стан: [вміст .ai/memory/state/project-state.yaml]
Останній handoff: [вміст .ai/logs/sessions/<остання-папка>/handoff.md]
```

Або у вигляді посилань, якщо агент має прямий доступ до репо:

```text
Прочитай:
- .ai/memory/state/project-state.yaml
- .ai/logs/sessions/<YYYY-MM-DD-topic>/handoff.md
```

### 3. Task (задача)

Використовуй task-промпти з `.ai/prompts/tasks/` або формулюй задачу самостійно.

Обов'язкові елементи задачі:

- **Що зробити** — конкретне, однозначне завдання.
- **Acceptance criteria** — чіткий чекліст "що вважається виконаним".
- **Артефакти** — які файли створити/оновити.

## Шаблони запитів

### Запит до Orchestrator (початок сесії)

```text
[System]: <вміст .ai/prompts/system/orchestrator.system.md>

Прочитай .ai/memory/state/project-state.yaml та останній handoff з .ai/logs/sessions/.

Поточна задача: <опис задачі>

Визнач:
1. Які агенти потрібні.
2. Порядок дій.
3. Acceptance criteria.
```

### Запит до Worker (виконання задачі)

```text
[System]: <вміст .ai/prompts/system/agent.worker.system.md>

Контекст: <стислий опис або посилання на handoff>

Задача: <FEAT-XXX> — <назва>

Acceptance criteria:
- [ ] <критерій 1>
- [ ] <критерій 2>

Артефакти для створення:
- <шлях/до/файлу.md>
```

### Запит до Reviewer (перевірка артефакту)

```text
[System]: <вміст .ai/prompts/system/agent.reviewer.system.md>

Перевір артефакт: <шлях/до/артефакту>
Тип: handoff package / ADR / документ

Чекліст: .ai/docs/04-quality-gates.md

Надай вердикт: approved / rejected (з обґрунтуванням).
```

### Запит до Researcher (дослідження теми)

```text
[System]: <вміст .ai/prompts/system/agent.researcher.system.md>

Питання: <дослідницький запит>

Зафіксуй результат у:
- .ai/memory/knowledge/<topic-notes.md>

Формат: факти / припущення / відкриті питання / рекомендація.
```

### Запит до Architect (архітектурне рішення)

```text
[System]: <вміст .ai/prompts/system/architect.system.md>

Питання/проблема: <опис>

Якщо приймається рішення:
- Створи ADR: .ai/memory/decisions/NNNN-<kebab-title>.md
- Оновити .ai/docs/01-architecture.md (якщо потрібно)
```

## Поради з ефективного запиту

1. **Один агент — одна роль**: не змішуй в одному запиті "зроби і перевір".
2. **Давай контекст явно**: агент не пам'ятає попередньої сесії без handoff.
3. **Фіксуй результат**: після кожного агента оновлюй project-state.yaml.
4. **Використовуй task-файли**: готові task-промпти у `.ai/prompts/tasks/` заощаджують час.
5. **Завжди закривай сесію** Handoff Package — інакше контекст буде втрачено.
