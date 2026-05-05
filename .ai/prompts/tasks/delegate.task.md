# Task: Delegate (Orchestrator → Agent)

Шаблон для явного делегування задачі від Orchestrator до конкретного агента.

## Вхідні дані (заповни перед відправкою)

- **Work item ID:** `<FEAT-XXX / IMPR-XXX / BUG-XXX>`
- **Назва задачі:** `<однорядковий заголовок>`
- **Агент-виконавець:** `[ ] worker  [ ] researcher  [ ] reviewer  [ ] architect`
- **Пріоритет:** `[ ] critical  [ ] high  [ ] medium  [ ] low`
- **Дедлайн (сесія):** `<YYYY-MM-DD або "поточна сесія">`

## Контекст

```text
Поточна фаза: <phase>
Остання сесія: .ai/logs/sessions/<YYYY-MM-DD-HHmm-topic>/
Посилання на handoff або ADR (якщо є): <шлях>
```

## Завдання

<Чіткий, однозначний опис — що саме потрібно зробити. Уникай "можливо" або "якщо треба".>

## Acceptance criteria

- [ ] `<критерій 1 — що саме перевіряємо>`
- [ ] `<критерій 2>`
- [ ] `<критерій 3>`

## Артефакти для створення / оновлення

- `<шлях/до/файлу.md>` — опис що в ньому
- `<шлях/до/іншого.yaml>`

## Обмеження

- Не змінюй файли поза переліченими артефактами без узгодження.
- Якщо задача потребує архітектурного рішення — ескалюй до Architect перед виконанням.

---

## Приклад заповнення

```markdown
- **Work item ID:** `IMPR-030`
- **Назва задачі:** Додати секцію Anti-patterns до системних промптів
- **Агент-виконавець:** [x] worker
- **Пріоритет:** [x] medium
- **Дедлайн:** поточна сесія

**Контекст:**
Поточна фаза: improve
Остання сесія: .ai/logs/sessions/2026-05-05-0200-improvements/

**Завдання:** Додати секцію `## Anti-patterns` до кожного з 5 системних промптів
у `.ai/prompts/system/`. Секція має містити мінімум 3 пункти.

**Acceptance criteria:**
- [ ] Усі 5 файлів містять секцію `## Anti-patterns`
- [ ] Кожна секція має ≥ 3 конкретних пункти
- [ ] Пункти відповідають ролі агента (не є копіями між файлами)

**Артефакти:**
- `.ai/prompts/system/agent.architect.system.md`
- `.ai/prompts/system/agent.orchestrator.system.md`
- `.ai/prompts/system/agent.worker.system.md`
- `.ai/prompts/system/agent.reviewer.system.md`
- `.ai/prompts/system/agent.researcher.system.md`
```
