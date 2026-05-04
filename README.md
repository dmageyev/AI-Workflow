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
   - [`.ai/start_promt.md`](./.ai/start_promt.md)

2. Інструкція до нього:
   - [`.ai/start_guide.md`](./.ai/start_guide.md)

3. Як робити запити до агентів:
   - [`.ai/docs/05-agent-requests.md`](./.ai/docs/05-agent-requests.md)

4. Базова архітектура та протокол handoff:
   - [`.ai/docs/01-architecture.md`](./.ai/docs/01-architecture.md)
   - [`.ai/docs/03-handoff-protocol.md`](./.ai/docs/03-handoff-protocol.md)

5. Перша сесія (мінімальний порядок):
   - Онови стан: [`.ai/memory/state/project-state.yaml`](./.ai/memory/state/project-state.yaml)
   - Створи папку сесії: `.ai/logs/sessions/YYYY-MM-DD-HHmm-topic/`
   - Додай туди:
     - `snapshot.yaml` (за шаблоном `.ai/prompts/handoff/snapshot.template.yaml`)
     - `handoff.md` (за шаблоном `.ai/prompts/handoff/handoff.template.md`)

## Структура репозиторію

```text
AI-Workflow/
  README.md
  llms.txt
  .gitignore
  .markdownlint.json
  .yamllint.yml

  .github/workflows/lint.yml

  .ai/
    start_promt.md
    start_guide.md
    create-repo-prompt.md

    docs/
      00-vision.md
      01-architecture.md
      02-workflow.md
      03-handoff-protocol.md
      04-quality-gates.md
      05-agent-requests.md

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

- `.ai/docs/` — бачення, архітектура, workflow, протокол передачі
- `.ai/prompts/` — системні промпти, task-промпти, handoff-шаблони
- `.ai/agents/` — реєстр агентів та ролі
- `.ai/memory/` — глосарій, knowledge base, ADR-рішення, проектний стан
- `.ai/workflows/` — runbook та приклади
- `.ai/logs/` — журнали сесій (Handoff Packages)
- `llms.txt` — опис репозиторію для LLM-інструментів

## Як працювати (операційна модель)

1. **Orchestrator** читає `.ai/memory/state/project-state.yaml` і останній handoff з `.ai/logs/sessions/`.
2. Делегує підзадачі агентам (Worker / Researcher / Reviewer).
3. Кожен результат оформлюється артефактами:
   - зміни в репо
   - ADR (якщо потрібні рішення) у `.ai/memory/decisions/`
   - оновлення `project-state.yaml`
   - новий Handoff Package у `.ai/logs/sessions/YYYY-MM-DD-HHmm-topic/`

## Quality Gates

Перед завершенням сесії переконайся, що виконано чекліст із:
[`.ai/docs/04-quality-gates.md`](./.ai/docs/04-quality-gates.md)

## CI / GitHub Actions

У репозиторії налаштовано GitHub Actions для перевірки:

- YAML (`yamllint`)
- Markdown (`markdownlint`)

Файл workflow: [`.github/workflows/lint.yml`](./.github/workflows/lint.yml)

---

> **Примітка:** Файл `start_promt.md` збережено з таким написанням навмисно (відповідно до вимоги).
