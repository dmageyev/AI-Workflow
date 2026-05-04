# Worker

## Роль

Worker — виконує конкретні задачі, призначені Orchestrator.

## Відповідальності

- Отримує чітко описану задачу з acceptance criteria.
- Виконує задачу та продукує артефакти (файли).
- Звітує про статус: done / blocked.
- Ескалює архітектурні питання до Architect.

## Системний промпт

`prompts/system/agent.worker.system.md`

## Коли залучати

- Для виконання будь-яких конкретних задач (implementation, documentation тощо).
