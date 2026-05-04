# Як адаптувати шаблон під свій проєкт

Цей документ описує, як перетворити `AI-Workflow` із загального шаблону
на робочий репозиторій для конкретного проєкту.

## Крок 1. Клонування або fork

Використай репозиторій як GitHub Template або зроби fork.
Не починай роботу безпосередньо в `dmageyev/AI-Workflow`.

## Крок 2. Оновлення `project-state.yaml`

Файл: [`memory/state/project-state.yaml`](../memory/state/project-state.yaml)

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

Файл: [`memory/glossary.uk.md`](../memory/glossary.uk.md)

Залиш базові терміни (Agent, Handoff, ADR тощо).
Додай терміни, специфічні для твоєї предметної галузі.

## Крок 4. Оновлення `domain-notes.md`

Файл: [`memory/knowledge/domain-notes.md`](../memory/knowledge/domain-notes.md)

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

1. Встанови реальні work items у [`memory/state/project-state.yaml`](../memory/state/project-state.yaml).
2. Створи папку першої сесії:
   [`logs/sessions/YYYY-MM-DD-HHmm-bootstrap/`](../logs/sessions/)
3. Заповни `snapshot.yaml` та `handoff.md` за шаблонами з [`prompts/handoff/`](../prompts/handoff/).
4. Закоміть — CI перевірить структуру сесії автоматично.

## Що НЕ потрібно змінювати

- [`docs/`](.) — документація архітектури та протоколів є універсальною.
- [`prompts/`](../prompts/) — системні та task-промпти є універсальними.
- [`agents/registry.yaml`](../agents/registry.yaml) — структура агентів є загальною (можна додати нові ролі).
- [`.github/workflows/lint.yml`](../../.github/workflows/lint.yml) — CI налаштовано правильно для будь-якого проєкту.

## Поради

- **Один репозиторій — один проєкт**: не намагайся вести кілька проєктів в одному репо.
- **Фіксуй всі рішення**: навіть дрібні архітектурні вибори варто записати як ADR.
- **Не пропускай handoff**: навіть при мінімальній сесії — завжди заповнюй Handoff Package.
