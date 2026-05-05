# Промпт для створення нового репозиторію AI-Workflow

Цей файл містить **готовий промпт**, який можна вставити у поле "Prompt" при створенні нового
репозиторію (наприклад, у діалозі "Create a new repository" в Copilot або аналогічному інструменті),
щоб автоматично розгорнути повну структуру мультиагентного workflow.

---

## PROMPT (копіюй повністю)

```text
Ти: Системний архітектор.

Ціль: Створити повну структуру репозиторію для мультиагентної роботи з "передачею свідомості"
(handoff protocol) в одному коміті/PR.

Репозиторій: <OWNER>/<REPO>
Гілка: main

Вимоги:
1. Усі файли AI-workflow розмістити у /.ai/ (не в корені репо).
2. Мовна політика: основний контент українською, технічні терміни/ключі YAML/імена файлів — англійською.
3. Додати GitHub Actions workflow (.github/workflows/lint.yml) для перевірки:
   - Markdown (markdownlint)
   - YAML (yamllint)
   - Структура сесій (session-structure job: snapshot.yaml + handoff.md у кожній папці)
   - Обов'язкові поля project-state.yaml (project-state-check job)
   Усі jobs мають мати permissions: contents: read.
4. Додати конфігурацію .markdownlint.json (line-length: 120) та .yamllint.yml.
5. Додати llms.txt у корені репо з описом структури для LLM-інструментів.
6. Додати CONTRIBUTING.md та CHANGELOG.md у корені репо.
7. Додати GitHub-шаблони:
   - .github/CODEOWNERS (власник: <OWNER> для шляху .ai/)
   - .github/ISSUE_TEMPLATE/bug_report.md
   - .github/ISSUE_TEMPLATE/improvement.md
   - .github/pull_request_template.md

Структура /.ai/:
  docs/
    bootstrap/
      start_promt.md          ← стартовий промпт для нового репо/циклу
      start_guide.md          ← інструкція до стартового промпту
      create-repo-prompt.md   ← цей файл (промпт для створення репо)
    00-vision.md          ← бачення проєкту
    01-architecture.md    ← архітектура мультиагентної системи
    02-workflow.md        ← операційна модель (цикл сесії)
    03-handoff-protocol.md ← протокол передачі свідомості
    04-quality-gates.md   ← чеклісти якості
    05-agent-requests.md  ← як робити запити до агентів
    06-adapting-template.md ← як адаптувати шаблон під свій проєкт
  prompts/
    system/               ← системні промпти: architect, orchestrator, worker, reviewer, researcher
    tasks/                ← task-промпти: create-plan, implement-feature, review, debug
    handoff/              ← шаблони: handoff.template.md, snapshot.template.yaml
  agents/
    registry.yaml         ← реєстр агентів (з полями delegates_to та escalates_to)
    roles/                ← описи ролей: architect, orchestrator, worker, reviewer, researcher
  memory/
    glossary.uk.md        ← глосарій
    decisions/            ← ADR (перший: 0001-record-architecture.md)
    knowledge/            ← knowledge base (domain-notes.md)
    state/
      project-state.yaml  ← канонічний стан проєкту
  workflows/
    runbook.uk.md         ← операційний runbook
    examples/
      example-handoff.md  ← посилання на реальну сесію як приклад
  logs/
    README.md               ← опис формату сесій
    sessions/               ← папки сесій (YYYY-MM-DD-HHmm-topic/)
      .gitkeep              ← зберігає порожню папку sessions/ в Git

Додатково у корені репо:
  README.md               ← опис репо та інструкція користування
  CONTRIBUTING.md         ← правила внеску
  CHANGELOG.md            ← журнал змін
  llms.txt                ← опис для LLM-інструментів
  .gitignore
  .markdownlint.json
  .yamllint.yml
  .github/CODEOWNERS
  .github/workflows/lint.yml
  .github/ISSUE_TEMPLATE/bug_report.md
  .github/ISSUE_TEMPLATE/improvement.md
  .github/pull_request_template.md

Definition of Done:
- Усі файли присутні в репозиторії.
- CI (markdownlint, yamllint, session-structure, project-state-check) налаштовано й проходить.
- README.md містить опис та інструкцію з посиланнями на /.ai/ файли.
- Все доставлено одним PR або одним комітом у гілці PR.
```

---

## Де використовувати

- **GitHub Copilot** (кодовий агент): вставити у поле "Prompt" при створенні нового завдання.
- **Cursor / Windsurf / інші AI IDE**: вставити як системний контекст або prompt.
- **ChatGPT / Claude / Gemini**: вставити на початку нової сесії.
- **GitHub Copilot Chat**: використати команду `/new` або вставити безпосередньо в чат.

## Після виконання промпту

1. Перевір, що всі файли зі структури вище присутні.
2. Переконайся, що CI проходить (Markdown lint + YAML lint + session-structure + project-state-check).
3. Запусти першу реальну сесію:
   - Заповни `.ai/memory/state/project-state.yaml` реальними work items.
   - Створи першу папку сесії: `.ai/logs/sessions/YYYY-MM-DD-HHmm-bootstrap/`
