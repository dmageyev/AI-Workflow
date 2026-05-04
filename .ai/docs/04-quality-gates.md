# Quality Gates

Перед завершенням кожної сесії перевір наступні чеклісти.

## Чекліст завершення сесії

- [ ] Створено папку сесії: [`logs/sessions/YYYY-MM-DD-HHmm-topic/`](../logs/sessions/)
- [ ] Створено `snapshot.yaml` (усі обов'язкові поля заповнені)
- [ ] Створено `handoff.md` (усі секції заповнені)
- [ ] Оновлено [`memory/state/project-state.yaml`](../memory/state/project-state.yaml) (статуси work items, фаза, прогрес)
- [ ] Усі нові архітектурні рішення зафіксовані ADR у [`memory/decisions/`](../memory/decisions/)
- [ ] Усі змінені/створені файли закомічені в репозиторій
- [ ] Acceptance criteria поточної сесії виконані

## Чекліст handoff.md

- [ ] Заповнена секція "Context" (включно з часом UTC)
- [ ] Заповнена секція "Session prompt" (текст промту + план)
- [ ] Заповнений чеклист "Goals"
- [ ] Заповнений чеклист "What was done"
- [ ] Є посилання на ADR (якщо були рішення)
- [ ] Є посилання на snapshot.yaml
- [ ] Перелічені open questions та blockers (або явно вказано "немає")
- [ ] Заповнені "Next actions" (принаймні 1 крок)
- [ ] Перелічені "Files changed / created"

## Чекліст snapshot.yaml

- [ ] `version` інкрементовано
- [ ] `date` відповідає даті сесії
- [ ] `time` відповідає часу сесії (UTC, формат HH:MM)
- [ ] `objective_ua` описує ціль сесії
- [ ] `state.phase` оновлено
- [ ] `state.progress` оновлено
- [ ] Усі `work_items` мають актуальний `status`

## Чекліст ADR (якщо приймалося рішення)

- [ ] Файл іменовано: [`memory/decisions/NNNN-kebab-case-title.md`](../memory/decisions/)
- [ ] Наявні секції: Context, Decision, Consequences, Status
- [ ] Рішення посилається з handoff.md

## Критерії відхилення handoff (Reviewer)

Reviewer може відхилити handoff, якщо:

- відсутній snapshot.yaml або handoff.md
- у handoff.md пропущені обов'язкові секції
- `project-state.yaml` не оновлено
- є незафіксовані архітектурні рішення
