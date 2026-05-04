# AI-Workflow

> **Мова контенту:** українська.
> **Технічні терміни/ключі/імена файлів:** англійською.

## Призначення

`AI-Workflow` — репозиторій-шаблон для **мультиагентної роботи** (Architect / Orchestrator / Worker / Reviewer / Researcher)
з формалізованою **передачею "свідомості"** між агентами.

Під "передачею свідомості" тут мається на увазі **Handoff Package** —
набір артефактів, які забезпечують безперервність роботи:

- `snapshot` (YAML): стан, цілі, обмеження, work items
- `handoff` (Markdown): підсумок, рішення, наступні кроки, посилання на файли

## Швидкий старт

1. Стартовий промпт для запуску нового репозиторію/циклу:
   - [`start_promt.md`](./start_promt.md)

2. Інструкція до нього:
   - [`start_guide.md`](./start_guide.md)

3. Базова архітектура та протокол handoff:
   - [`docs/01-architecture.md`](./docs/01-architecture.md)
   - [`docs/03-handoff-protocol.md`](./docs/03-handoff-protocol.md)

4. Перша сесія (мінімальний порядок):
   - Онови стан: [`memory/state/project-state.yaml`](./memory/state/project-state.yaml)
   - Створи папку сесії: `logs/sessions/YYYY-MM-DD-topic/`
   - Додай туди:
     - `snapshot.yaml` (за шаблоном `prompts/handoff/snapshot.template.yaml`)
     - `handoff.md` (за шаблоном `prompts/handoff/handoff.template.md`)

## Структура репозиторію

```text
AI-Workflow/
  README.md
  start_promt.md
  start_guide.md
  .gitignore
  .markdownlint.json
  .yamllint.yml

  .github/workflows/lint.yml

  docs/
    00-vision.md
    01-architecture.md
    02-workflow.md
    03-handoff-protocol.md
    04-quality-gates.md

  prompts/
    system/
      architect.system.md
      orchestrator.system.md
      agent.worker.system.md
      agent.reviewer.system.md
      agent.researcher.system.md
    tasks/
      create-plan.task.md
      implement-feature.task.md
      review.task.md
      debug.task.md
    handoff/
      handoff.template.md
      snapshot.template.yaml

  agents/
    registry.yaml
    roles/
      architect.md
      orchestrator.md
      worker.md
      reviewer.md
      researcher.md

  memory/
    glossary.uk.md
    decisions/
      0001-record-architecture.md
    knowledge/
      domain-notes.md
    state/
      project-state.yaml

  workflows/
    runbook.uk.md
    examples/
      example-handoff.md

  logs/
    sessions/
      README.md
```

- `docs/` — бачення, архітектура, workflow, протокол передачі
- `prompts/` — системні промпти, task-промпти, handoff-шаблони
- `agents/` — реєстр агентів та ролі
- `memory/` — глосарій, knowledge base, ADR-рішення, проектний стан
- `workflows/` — runbook та приклади
- `logs/` — журнали сесій (Handoff Packages)

## Як працювати (операційна модель)

1. **Orchestrator** читає `memory/state/project-state.yaml` і останній handoff з `logs/sessions/`.
2. Делегує підзадачі агентам (Worker / Researcher / Reviewer).
3. Кожен результат оформлюється артефактами:
   - зміни в репо
   - ADR (якщо потрібні рішення) у `memory/decisions/`
   - оновлення `project-state.yaml`
   - новий Handoff Package у `logs/sessions/YYYY-MM-DD-topic/`

## Quality Gates

Перед завершенням сесії переконайся, що виконано чекліст із:
[`docs/04-quality-gates.md`](./docs/04-quality-gates.md)

## CI / GitHub Actions

У репозиторії налаштовано GitHub Actions для перевірки:

- YAML (`yamllint`)
- Markdown (`markdownlint`)

Файл workflow: [`.github/workflows/lint.yml`](./.github/workflows/lint.yml)

---

> **Примітка:** Файл `start_promt.md` збережено з таким написанням навмисно (відповідно до вимоги).
