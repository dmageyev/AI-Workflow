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

### Правило архівації після milestone

Після завершення кожного milestone:

1. Перенеси всі done-items з `work_items` (крім останнього) до
   [`.ai/memory/state/work-items-archive.yaml`](../memory/state/work-items-archive.yaml).
2. Додай новий блок у `milestones`:

   ```yaml
   - id: "your-milestone-name"
     closed_at: "YYYY-MM-DD"
     items:
       - id: "FEAT-001"
         title: "..."
         status: "done"
         notes: "..."
   ```

3. Останній done-item залишається у `work_items` як breadcrumb
   (орієнтир для наступного агента, звідки продовжувати).
4. CI (`work-items-archive-check`) автоматично перевіряє, що всі items у архіві мають `status: done`.

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

## Робота в команді

Цей розділ описує, як адаптувати AI-Workflow для команди з кількох людей.

### Ownership моделі

| Модель | Опис | Коли підходить |
|--------|------|----------------|
| **Single Orchestrator** | Одна людина — Orchestrator, решта — Workers | Команда ≤ 3 людини |
| **Rotating Orchestrator** | Orchestrator змінюється між сесіями (черговість) | Команда 3-5 людини |
| **Shared Orchestrator** | Кілька Orchestrator, кожен відповідає за свій домен | Велика команда |

### CODEOWNERS для команди

Файл [`.github/CODEOWNERS`](../../.github/CODEOWNERS) — визначає хто reviewer для яких шляхів.

Приклад для команди 3-5 людей:

```text
# Загальний review для всього .ai/
.ai/ @team-lead

# Архітектурні рішення — мінімум 2 reviewer
.ai/memory/decisions/ @architect-1 @architect-2

# Стан проєкту — тільки Orchestrator
.ai/memory/state/ @orchestrator-username

# Документація — будь-який член команди
.ai/docs/ @your-org/team-name
```

### Запобігання race conditions на project-state.yaml

`project-state.yaml` — єдиний файл, що може стати джерелом конфліктів при паралельній роботі.

**Правила:**

1. **Один Orchestrator за раз**: тільки один член команди виступає Orchestrator у поточній сесії.
2. **Branch per session**: кожна сесія — окрема гілка. Merge у `main` тільки після закриття сесії.
3. **PR review для state змін**: будь-яка зміна `project-state.yaml` потребує PR + review від
   іншого члена команди.
4. **Conflict resolution**: при merge конфлікті у `project-state.yaml` — беруть за основу
   вищий `version`. Нижчий version — merge вручну.

### Синхронізація між сесіями (async-команда)

Якщо команда працює асинхронно (різні часові зони):

1. Перед початком сесії обов'язково читай останній handoff
   (`git pull` + `.ai/logs/sessions/<остання>/handoff.md`).
2. Свою сесію починай лише після того, як попередня закрита
   (обидва файли: `snapshot.yaml` + `handoff.md` присутні).
3. Використовуй `## Open questions` у handoff для асинхронних питань до команди.

### Checklist для командного використання

- [ ] CODEOWNERS налаштовано для всіх критичних шляхів
- [ ] Визначено хто є Orchestrator (або розклад ротації)
- [ ] Прийнято правило "branch per session"
- [ ] Увімкнено branch protection для `main` (require PR + review)
- [ ] Команда ознайомлена з протоколом handoff

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
