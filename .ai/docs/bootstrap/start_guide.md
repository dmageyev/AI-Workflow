# Start Guide

Цей документ пояснює, **як використовувати** [`start_promt.md`](./start_promt.md) для запуску нового репозиторію
або нового циклу робіт у `AI-Workflow`.

## Коли використовувати

- Ти щойно створив(ла) репозиторій і хочеш швидко розгорнути структуру.
- Ти хочеш "перезапустити" процес після паузи і відновити контекст.
- Ти переносиш workflow у інший репозиторій (копіюєш структуру як template).

## Як використовувати (кроки)

1. Відкрий [`start_promt.md`](./start_promt.md).
2. Заміни плейсхолдери:
   - `<OWNER>/<REPO>` на реальне значення (наприклад, `dmageyev/AI-Workflow`).
3. Встав промпт у чат з LLM (або інструментом-агентом).
4. Попроси агента:
   - створити/оновити файли,
   - оформити перший **Handoff Package**.

## Який результат очікувати

Після виконання промпта у репозиторії мають бути:

- актуальний стан у [`memory/state/project-state.yaml`](../../memory/state/project-state.yaml)
- описані ролі/реєстр у [`agents/registry.yaml`](../../agents/registry.yaml)
- описаний протокол передачі у [`docs/03-handoff-protocol.md`](../03-handoff-protocol.md)
- готовий runbook у [`workflows/runbook.uk.md`](../../workflows/runbook.uk.md)
- створена перша сесія у [`logs/sessions/`](../../logs/sessions/)`YYYY-MM-DD-HHmm-topic/` (якщо агент має право комітити)

## Якщо агент не має права комітити

Попроси його:

- згенерувати вміст файлів у повідомленні,
- а ти вже вручну додай файли в репозиторій.

## Мінімальний "перший handoff" вручну

1. Створи папку: [`logs/sessions/`](../../logs/sessions/)`YYYY-MM-DD-HHmm-bootstrap/`
2. Додай:
   - `snapshot.yaml` (копія [`prompts/handoff/snapshot.template.yaml`](../../prompts/handoff/snapshot.template.yaml) + заповнити)
   - `handoff.md` (копія [`prompts/handoff/handoff.template.md`](../../prompts/handoff/handoff.template.md) + заповнити)
3. Закоміть.

## Порада по дисципліні пам'яті

- Все тимчасове — у [`logs/`](../../logs/).
- Все довготривале — у [`memory/`](../../memory/).
- Рішення — тільки ADR у [`memory/decisions/`](../../memory/decisions/).
