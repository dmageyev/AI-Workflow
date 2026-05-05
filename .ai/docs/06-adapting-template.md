# Як адаптувати шаблон під свій проєкт

Цей документ описує, як перетворити `AI-Workflow` із загального шаблону
на робочий репозиторій для конкретного проєкту.

## Крок 1. Клонування або fork

Використай репозиторій як GitHub Template або зроби fork.
Не починай роботу безпосередньо в `dmageyev/AI-Workflow`.

## Крок 2. Оновлення `project-state.yaml`

Файл: [`.ai/memory/state/project-state.yaml`](../memory/state/project-state.yaml)

Замін:

| Поле | Що змінити |
| ---- | ---------- |
| `project` | Назва твого проєкту |
| `owner` | Твій GitHub username або організація |
| `objective_ua` | Мета проєкту однією фразою |
| `current_focus` | Поточний фокус (наприклад, "bootstrap") |
| `state.phase` | Початкова фаза: `"bootstrap"` |
| `state.progress` | Початковий прогрес: `0` |
| `work_items` | Видали BOOT/IMPR items, додай власні задачі |

Формат work item:

```yaml
- id: "FEAT-001"
  title: "Назва задачі"
  status: "todo"
  notes: "Опис або контекст"
```

## Крок 3. Оновлення глосарію

Файл: [`.ai/memory/glossary.uk.md`](../memory/glossary.uk.md)

Залиш базові терміни (Agent, Handoff, ADR тощо).
Додай терміни, специфічні для твоєї предметної галузі.

## Крок 4. Оновлення `domain-notes.md`

Файл: [`.ai/memory/knowledge/domain-notes.md`](../memory/knowledge/domain-notes.md)

Заміни placeholder-контент на реальні знання про твій домен:

- Ключові концепції предметної галузі.
- Технічні обмеження та залежності.
- Посилання на зовнішні специфікації або документацію.

## Крок 5. CODEOWNERS

Файл: [`.github/CODEOWNERS`](../../.github/CODEOWNERS)

Заміни `@dmageyev` на свій GitHub username або команду:

```text
.ai/ @your-username
```

## Крок 6. Перша реальна сесія

1. Встанови реальні work items у [`.ai/memory/state/project-state.yaml`](../memory/state/project-state.yaml).
2. Створи папку першої сесії:
   [`.ai/logs/sessions/YYYY-MM-DD-HHmm-bootstrap/`](../logs/sessions/)
3. Заповни `snapshot.yaml` та `handoff.md` за шаблонами з [`.ai/prompts/handoff/`](../prompts/handoff/).
4. Закоміть — CI перевірить структуру сесії автоматично.

## Що НЕ потрібно змінювати

- [`.ai/docs/`](.) — документація архітектури та протоколів є універсальною.
- [`.ai/prompts/`](../prompts/) — системні та task-промпти є універсальними.
- [`.ai/agents/registry.yaml`](../agents/registry.yaml) — структура агентів є загальною (можна додати нові ролі).
- [`.github/workflows/lint.yml`](../../.github/workflows/lint.yml) — CI налаштовано правильно для будь-якого проєкту.

## Поради

- **Один репозиторій — один проєкт**: не намагайся вести кілька проєктів в одному репо.
- **Фіксуй всі рішення**: навіть дрібні архітектурні вибори варто записати як ADR.
- **Не пропускай handoff**: навіть при мінімальній сесії — завжди заповнюй Handoff Package.

## GitHub Discussions (опціонально)

GitHub Discussions — зручний простір для нефіксованих роздумів, запитань та асинхронного
спілкування навколо проєкту.

**Коли вмикати:**

- Якщо над репозиторієм працює більше однієї людини або команди.
- Для збору зворотнього зв'язку щодо архітектурних рішень перед тим, як вони стануть ADR.
- Для логування "м'яких" рішень, що не потребують формального ADR.

**Як активувати:**

1. Перейди до `Settings → General → Features` у своєму репозиторії.
2. Увімкни `Discussions`.
3. Рекомендовані категорії: `General`, `Ideas`, `Q&A`, `ADR Proposals`.

**Зв'язок з ADR-процесом:**

- Discussion може стати стартовим майданчиком для ADR: після досягнення консенсусу — оформлюй
  як `NNNN-kebab-case-title.md` у [`.ai/memory/decisions/`](../memory/decisions/).
- Посилання на Discussion можна додати у секцію `## Context` ADR для збереження передісторії.
