# Приклад Handoff Package

Ця папка ілюструє, як виглядає реальний Handoff Package після завершення сесії.

## Структура прикладу

```text
.ai/logs/sessions/2026-05-04-1200-bootstrap/
  snapshot.yaml
  handoff.md
```

---

## Приклад: handoff.md

```markdown
# Handoff Package

## Context (UA)

- **Project:** AI-Workflow
- **Date:** 2026-05-04
- **Topic:** bootstrap
- **Session folder:** .ai/logs/sessions/2026-05-04-1200-bootstrap/

## Goals

- [x] Розгорнути повну структуру репозиторію
- [x] Додати GitHub Actions lint (Markdown + YAML)
- [x] Створити README.md, start_promt.md, start_guide.md

## What was done

- [x] Створено всі директорії та файли згідно повної структури
- [x] Налаштовано .github/workflows/lint.yml
- [x] Написано README.md з описом та інструкцією
- [x] Написано start_promt.md та start_guide.md
- [x] Заповнено .ai/memory/state/project-state.yaml

## Key decisions

- Decision links: .ai/memory/decisions/0001-record-architecture.md

## Current state

- **Snapshot:** .ai/logs/sessions/2026-05-04-1200-bootstrap/snapshot.yaml
- **Open questions:** немає
- **Blockers:** немає

## Next actions (ordered)

1. Розпочати першу реальну сесію з реальними work items
2. Оновити project-state.yaml з новими задачами
3. При необхідності — додати нові ADR

## Files changed / created

- README.md
- .ai/start_promt.md
- .ai/start_guide.md
- .github/workflows/lint.yml
- (та всі інші файли структури)

## Acceptance criteria

- [x] Усі файли присутні в репозиторії
- [x] CI (markdownlint, yamllint) налаштовано
- [x] Доставлено одним PR
```

---

## Приклад: snapshot.yaml

```yaml
version: 1
project: "AI-Workflow"
date: "2026-05-04"
owner: "dmageyev"

objective_ua: "Розгортання повної структури репозиторію"
current_focus: "bootstrap complete"

agents:
  active:
    - "orchestrator"
  available:
    - "architect"
    - "worker"
    - "reviewer"
    - "researcher"

state:
  phase: "bootstrap"
  progress: 100

work_items:
  - id: "BOOT-001"
    title: "Create repo structure"
    status: "done"
    notes: "Повна структура розгорнута одним PR"
```
