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

- `.ai/prompts/handoff/handoff.template.md`
- `.ai/prompts/handoff/snapshot.template.yaml`

## Правила версіонування

- `version` у snapshot.yaml інкрементується при кожному новому handoff у рамках одного topic.
- Якщо topic змінюється — нова папка, `version` починається з 1.
- Посилатися на конкретний handoff: шлях до папки сесії + `#` якір до секції.
