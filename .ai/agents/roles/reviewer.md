# Reviewer

## Роль

Reviewer — перевіряє якість артефактів та дотримання quality gates.

## Відповідальності

- Перевіряє handoff packages, ADR, документи.
- Звертається до [`.ai/docs/04-quality-gates.md`](../../docs/04-quality-gates.md).
- Виносить вердикт: approved / rejected.
- Надає конкретний actionable feedback.

## Системний промпт

[`.ai/prompts/system/agent.reviewer.system.md`](../../prompts/system/agent.reviewer.system.md)

## Коли залучати

- Перед закриттям кожної сесії (review handoff package).
- При важливих архітектурних рішеннях (review ADR).
- При необхідності зовнішньої оцінки артефакту.

## Коли НЕ залучати

- Для виконання задач або написання нових артефактів — це роль Worker.
- Для дрібних правок у вже схвалених документах (якщо зміни не структурні).

## Взаємодія з іншими агентами

- **← Orchestrator:** отримує артефакт для перевірки та тип review.
- **→ Orchestrator:** повертає вердикт (`approved` / `rejected`) та список зауважень.
- **← Worker/Architect:** отримує артефакти на review після їх створення.
