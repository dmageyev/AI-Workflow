# Runbook: Операційна інструкція

Цей документ описує, як реально працювати з репозиторієм `AI-Workflow` у щоденному режимі.

## 1. Запуск нової сесії

1. Прочитай `memory/state/project-state.yaml`.
2. Знайди останню папку у `logs/sessions/` (сортування за датою).
3. Прочитай `handoff.md` з цієї папки.
4. Перевір open questions та blockers.
5. Визнач work items для поточної сесії.

## 2. Вибір агентів

На основі work items визнач, які агенти потрібні:

| Задача | Агент |
| ------ | ----- |
| Архітектурне рішення | Architect |
| Координація сесії | Orchestrator |
| Виконання задачі | Worker |
| Перевірка артефактів | Reviewer |
| Дослідження теми | Researcher |

## 3. Виконання задач

1. Orchestrator делегує задачі агентам.
2. Кожен агент використовує свій системний промпт із `prompts/system/`.
3. Для типових задач — використовуй task-промпти з `prompts/tasks/`.
4. Усі артефакти зберігати у репо (не в чаті).

## 4. Закриття сесії

1. Створи папку: `logs/sessions/YYYY-MM-DD-topic/`
2. Заповни `snapshot.yaml` (шаблон: `prompts/handoff/snapshot.template.yaml`).
3. Заповни `handoff.md` (шаблон: `prompts/handoff/handoff.template.md`).
4. Оновити `memory/state/project-state.yaml`.
5. Перевір quality gates: `docs/04-quality-gates.md`.
6. Закоміть усі зміни.

## 5. Escalation paths

| Ситуація | Дія |
| -------- | --- |
| Архітектурне питання | Залучити Architect |
| Blocker без вирішення | Зафіксувати в handoff.md, залучити власника |
| Reviewer відхилив | Виправити зауваження, повторно подати |
| Невизначеність у задачі | Уточнити у Orchestrator, не починати виконання |

## 6. Іменування файлів та папок

- Папки сесій: `YYYY-MM-DD-kebab-case-topic`
- ADR файли: `NNNN-kebab-case-title.md`
- Артефакти: snake\_case або kebab-case, розширення `.md` або `.yaml`
