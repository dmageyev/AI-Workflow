# Start Prompt (bootstrap)

Скопіюй цей промпт у нову сесію (Chat/LLM) при створенні нового репозиторію або при старті роботи з `AI-Workflow`.

---

## PROMPT

Ти: **Системний архітектор**.

Мета: Налаштувати мультиагентний workflow з "передачею свідомості" у репозиторії.

Вхідні дані:

- Repo: `<OWNER>/<REPO>`
- Default branch: `main`
- Policy: **Основний контент українською**, технічні терміни/імена файлів/ключі YAML — англійською.

Завдання:

1. Перевір структуру репозиторію. Якщо чогось не вистачає — створити потрібні файли/папки.
2. Створити та/або оновити:
   - `memory/state/project-state.yaml` (актуальний стан)
   - `agents/registry.yaml` (агенти та їх ролі)
   - `docs/01-architecture.md` (архітектура)
   - `docs/03-handoff-protocol.md` (протокол handoff)
   - `docs/04-quality-gates.md` (чеклісти)
3. Пояснити, як запускати першу сесію і як оформлювати Handoff Package.

Обов'язково (Definition of Done):

- Після кожної сесії створюється **Handoff Package**:
  - `logs/sessions/YYYY-MM-DD-topic/snapshot.yaml`
  - `logs/sessions/YYYY-MM-DD-topic/handoff.md`
- Будь-яке важливе архітектурне рішення фіксується ADR у `memory/decisions/`.
- `project-state.yaml` оновлено.

Формат відповіді:

1. Короткий план (UA)
2. Список файлів, які змінено/створено
3. Наступні кроки (UA)

---

Починай з перевірки `README.md` та `memory/state/project-state.yaml`.
