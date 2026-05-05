# Contributing to AI-Workflow

Дякуємо, що розглядаєте можливість внеску в цей шаблон репозиторію!

## Що можна покращувати

- Промпти агентів (`.ai/prompts/`)
- Документацію та протоколи (`.ai/docs/`)
- Ролі агентів (`.ai/agents/roles/`)
- Workflows та runbook (`.ai/workflows/`)
- CI/CD конфігурацію (`.github/workflows/`)

## Правила внеску

### Мовна політика

- Контент (пояснення, описи): **Українська**
- Технічні терміни, YAML-ключі, назви файлів: **Англійська**

### Структура репозиторію

- Усі артефакти зберігаються під `.ai/` — не створюй нові кореневі директорії без ADR.
- Назви файлів: `kebab-case` для Markdown і YAML.
- Нові архітектурні рішення — фіксуй як ADR у `.ai/memory/decisions/NNNN-kebab-case.md`.

### Комміти

- Формат: `<type>: <short description>` (англійською)
- Типи: `feat`, `fix`, `docs`, `refactor`, `chore`, `ci`
- Приклад: `docs: add few-shot examples to orchestrator system prompt`

### Pull Request

1. Переконайся, що CI проходить (`markdownlint` + `yamllint`).
2. Заповни шаблон PR.
3. Якщо PR змінює протоколи або структуру — додай посилання на ADR.

### Нові агенти

Щоб додати нового агента:

1. Створи role-файл: `.ai/agents/roles/<name>.md`
2. Створи системний промпт: `.ai/prompts/system/agent.<name>.system.md`
3. Додай агента до `.ai/agents/registry.yaml`
4. Зафіксуй рішення як ADR

### Нові task-промпти

1. Створи файл: `.ai/prompts/tasks/<name>.task.md`
2. Дотримуйся структури: вхідні дані → завдання → очікуваний результат → приклад заповнення

## Локальна перевірка

```bash
# Markdown
npm install -g markdownlint-cli
markdownlint "**/*.md" --ignore node_modules

# YAML
pip install yamllint
yamllint -c .yamllint.yml .
```

## Питання

Відкрий issue з міткою `question` або `improvement`.
