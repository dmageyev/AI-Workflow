# Task: Review

## Вхідні дані (заповни перед відправкою)

- **Артефакт для review:** `<шлях до файлу або папки>`
- **Тип review:** `[ ] handoff package  [ ] ADR  [ ] документ  [ ] код`
- **Чеклист:** [`docs/04-quality-gates.md`](../../docs/04-quality-gates.md)

## Завдання для агента (Reviewer)

1. Відкрий артефакт.
2. Перевір за відповідним чеклістом із [`docs/04-quality-gates.md`](../../docs/04-quality-gates.md).
3. Зафіксуй усі знайдені проблеми (файл + опис).
4. Винеси вердикт: `approved` або `rejected`.

## Очікуваний результат

- Список проблем (або "немає зауважень").
- Вердикт: `approved` / `rejected`.
- Якщо `rejected` — чіткий перелік того, що потрібно виправити.

---

## Приклад заповнення

```markdown
- **Артефакт для review:** `.ai/logs/sessions/2026-05-04-2200-bootstrap/`
- **Тип review:** [x] handoff package
- **Чеклист:** `.ai/docs/04-quality-gates.md`
```

Очікувана відповідь агента:

```markdown
Вердикт: approved

Зауваження: немає. Обидва файли (snapshot.yaml, handoff.md) присутні,
усі обов'язкові секції заповнені, project-state.yaml оновлено.
```
