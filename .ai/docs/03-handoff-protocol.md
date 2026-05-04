# Протокол Handoff ("передача свідомості")

## Що таке Handoff Package

Handoff Package — це набір артефактів, що передають повний контекст між агентами або між сесіями.

Складається з двох обов'язкових файлів:

1. `snapshot.yaml` — машинозчитуваний стан (structured state)
2. `handoff.md` — людиночитаний підсумок (narrative summary)

## Структура папки сесії

```text
.ai/logs/sessions/YYYY-MM-DD-HHmm-topic/
  snapshot.yaml
  handoff.md
  [опційно: artifact-1.md, artifact-2.yaml, ...]
```

## Обов'язкові поля snapshot.yaml

| Поле | Тип | Опис |
| ---- | --- | ---- |
| `version` | integer | Версія снапшота (починається з 1) |
| `project` | string | Назва проєкту |
| `date` | string | Дата у форматі YYYY-MM-DD |
| `time` | string | Час у форматі HH:MM (UTC) |
| `owner` | string | Відповідальний |
| `objective_ua` | string | Ціль поточної сесії (UA) |
| `current_focus` | string | Що зараз у фокусі |
| `agents.active` | list | Активні агенти в сесії |
| `state.phase` | string | Фаза проєкту |
| `state.progress` | integer | Відсоток виконання (0-100) |
| `work_items` | list | Список задач з id, title, status |

## Правила handoff.md

- Секція "Context" — коротко хто/що/де/коли (UA), включно з часом сесії (UTC).
- Секція "Session prompt" — текст промту та як агент його зрозумів.
- Секція "Goals" — чеклист цілей сесії.
- Секція "What was done" — чеклист виконаного.
- Секція "Key decisions" — посилання на ADR файли.
- Секція "Current state" — посилання на snapshot.yaml, open questions, blockers.
- Секція "Next actions" — пронумерований список наступних кроків.
- Секція "Files changed / created" — список шляхів.
- Секція "Acceptance criteria" — чеклист критеріїв прийняття.

## Шаблони

- [`prompts/handoff/handoff.template.md`](../prompts/handoff/handoff.template.md)
- [`prompts/handoff/snapshot.template.yaml`](../prompts/handoff/snapshot.template.yaml)

## Правила версіонування

- `version` у snapshot.yaml інкрементується при кожному новому handoff у рамках одного topic.
- Якщо topic змінюється — нова папка, `version` починається з 1.
- Посилатися на конкретний handoff: шлях до папки сесії + `#` якір до секції.

## Протокол відновлення після збою

Якщо сесія перервалася до створення Handoff Package:

1. **Детекція незакритої сесії.** Orchestrator на початку перевіряє: чи існує папка в
   [`logs/sessions/`](../logs/sessions/), яка не містить обох файлів (`snapshot.yaml` та `handoff.md`).
   Якщо так — попередня сесія вважається незакритою.

2. **Мінімальний аварійний handoff.** Якщо завершити повноцінний handoff неможливо,
   необхідно створити файл `handoff.md` з позначкою:

   ```markdown
   > ⚠️ АВАРІЙНЕ ЗАВЕРШЕННЯ СЕСІЇ
   > Сесія перервалась до створення повного Handoff Package.
   > Відновіть стан з git log та `.ai/memory/state/project-state.yaml`.
   ```

3. **Відновлення контексту.** Наступна сесія повинна:
   - Прочитати [`memory/state/project-state.yaml`](../memory/state/project-state.yaml) як canonical state
   - Перевірити `git log` на останні зміни
   - Зафіксувати незакриту попередню сесію в секції "Open questions" нового handoff

4. **Правило: незакрита сесія блокує нову.** Orchestrator не делегує нові задачі, доки
   не буде закрита незакрита сесія (хоча б мінімальним аварійним handoff).

## Різниця між snapshot.yaml і project-state.yaml

| | `snapshot.yaml` | `project-state.yaml` |
|---|---|---|
| **Розташування** | [`logs/sessions/`](../logs/sessions/)`<session>/` | [`memory/state/`](../memory/state/) |
| **Призначення** | Зріз стану однієї конкретної сесії | Живий канонічний стан усього проєкту |
| **Мутабельність** | Незмінний після закриття сесії | Оновлюється Orchestrator після кожної сесії |
| **Читається** | Наступним агентом при відновленні контексту | Orchestrator на початку кожної сесії |
| **Зберігається** | Назавжди (частина інституційної пам'яті) | Відображає поточний момент |
