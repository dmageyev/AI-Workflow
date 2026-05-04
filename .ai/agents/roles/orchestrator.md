# Orchestrator

## Роль

Orchestrator — координує роботу всіх агентів і забезпечує цілісність стану між сесіями.

## Відповідальності

- Читає project-state.yaml та останній handoff перед кожною сесією.
- Делегує задачі Worker, Researcher, Reviewer.
- Оновлює project-state.yaml після кожної сесії.
- Створює Handoff Package в logs/sessions/.

## Системний промпт

`prompts/system/orchestrator.system.md`

## Коли залучати

- На початку кожної сесії (відновлення контексту).
- При координації кількох агентів на одну задачу.
- При завершенні сесії (закриття handoff).
