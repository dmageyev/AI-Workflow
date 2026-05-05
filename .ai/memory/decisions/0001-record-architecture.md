# ADR-0001: Базова архітектура репозиторію

## Status

`accepted`

## Date

2026-05-04

## Context

Потрібна базова структура репозиторію для мультиагентної роботи з передачею контексту між сесіями.
Потрібно вирішити: як організувати файли, як зберігати стан, як формалізувати handoff.

## Decision

Прийнято наступну структуру:

- [`.ai/docs/`](../../docs/) — документація архітектури та протоколів
- [`.ai/prompts/`](../../prompts/) — системні та task-промпти для агентів
- [`.ai/agents/`](../../agents/) — реєстр та описи ролей
- [`.ai/memory/`](../../memory/) — довготривала пам'ять (glossary, knowledge, decisions, state)
- [`.ai/workflows/`](../../workflows/) — runbook та приклади
- [`.ai/logs/sessions/`](../../logs/sessions/) — журнал сесій (Handoff Packages)

Handoff Package складається з `snapshot.yaml` (YAML state) + `handoff.md` (narrative summary).

Мовна політика: основний контент українською, технічні терміни/ключі/файли — англійською.

## Consequences

- Усі агенти працюють через артефакти в репо (не через прямі повідомлення).
- Orchestrator є єдиним власником [`memory/state/project-state.yaml`](../state/project-state.yaml).
- Кожна сесія обов'язково завершується Handoff Package.
- ADR фіксуються у [`memory/decisions/`](.) за схемою `NNNN-kebab-case-title.md`.
