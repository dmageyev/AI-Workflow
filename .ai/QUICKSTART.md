# Quickstart — AI-Workflow

5 кроків від нуля до першої повноцінної сесії.

---

## Крок 1. Fork або Template

Натисни **"Use this template"** на GitHub або зроби fork `dmageyev/AI-Workflow`.

> Не працюй безпосередньо в оригінальному репозиторії.

---

## Крок 2. Налаштуй project-state.yaml

Відкрий [`memory/state/project-state.yaml`](./memory/state/project-state.yaml)
і заміни значення під свій проєкт:

```yaml
project: "Назва твого проєкту"
owner: "твій-github-username"
objective_ua: "Ціль проєкту одним реченням"
state:
  phase: "bootstrap"
  progress: 0
work_items:
  - id: "BOOT-001"
    title: "Перша задача"
    status: "todo"
    notes: ""
```

Детальна інструкція: [`docs/06-adapting-template.md`](./docs/06-adapting-template.md)

---

## Крок 3. Налаштуй CODEOWNERS

Відкрий [`../.github/CODEOWNERS`](../.github/CODEOWNERS) і заміни `@dmageyev` на свій username:

```text
.ai/ @твій-username
```

---

## Крок 4. Запусти першу сесію

### 4.1. Обери роль агента

Завантаж системний промпт відповідно до своєї задачі:

| Якщо тобі потрібно... | Використай агента |
| --- | --- |
| Скоординувати роботу | [Orchestrator](./prompts/system/agent.orchestrator.system.md) |
| Виконати конкретну задачу | [Worker](./prompts/system/agent.worker.system.md) |
| Дослідити тему | [Researcher](./prompts/system/agent.researcher.system.md) |
| Перевірити артефакт | [Reviewer](./prompts/system/agent.reviewer.system.md) |
| Прийняти архітектурне рішення | [Architect](./prompts/system/agent.architect.system.md) |

### 4.2. Структура запиту до агента

```text
[System]: <вміст файлу системного промпту>

Прочитай:
- .ai/memory/state/project-state.yaml

Задача: <опис твоєї задачі>
Acceptance criteria:
- [ ] <що вважається виконаним>
```

Детальніше: [`docs/05-agent-requests.md`](./docs/05-agent-requests.md)

---

## Крок 5. Закрий сесію (Handoff Package)

Після кожної сесії створи папку і два файли:

```text
.ai/logs/sessions/YYYY-MM-DD-HHmm-topic/
  snapshot.yaml   ← за шаблоном .ai/prompts/handoff/snapshot.template.yaml
  handoff.md      ← за шаблоном .ai/prompts/handoff/handoff.template.md
```

Оновити [`memory/state/project-state.yaml`](./memory/state/project-state.yaml)
(статуси work items, фаза, прогрес).

Закоміть — CI автоматично перевірить структуру сесії.

---

## Bootstrap checklist (перша сесія)

- [ ] Fork/template створено
- [ ] `project-state.yaml` оновлено (project, owner, objective_ua, work_items)
- [ ] `CODEOWNERS` оновлено
- [ ] Перший запит до агента сформульовано (system prompt + task)
- [ ] Папку сесії створено: `.ai/logs/sessions/YYYY-MM-DD-HHmm-bootstrap/`
- [ ] `snapshot.yaml` заповнено (усі обов'язкові поля)
- [ ] `handoff.md` заповнено (усі секції)
- [ ] Зміни закомічено, CI пройшов

---

## Корисні посилання

- [Архітектура системи](./docs/01-architecture.md)
- [Workflow (цикл сесії)](./docs/02-workflow.md)
- [Протокол Handoff](./docs/03-handoff-protocol.md)
- [Quality Gates](./docs/04-quality-gates.md)
- [Запити до агентів](./docs/05-agent-requests.md)
- [Адаптація під свій проєкт](./docs/06-adapting-template.md)
- [Глосарій](./memory/glossary.uk.md)
