# Handoff Package — SCALE-005

## Context (UA)

- **Project:** AI-Workflow
- **Date:** 2026-05-05
- **Time (UTC):** 02:31
- **Topic:** scale-005
- **Session folder:** [`.ai/logs/sessions/2026-05-05-0231-scale-005/`](.)

## Session prompt

**Text:**

> SCALE-005 — Consolidate template root files into .ai/ directory

**Plan:**

Виконати SCALE-005: перемістити файли шаблону (STATUS.md, ROADMAP.md, QUICKSTART.md, VERSION)
з кореня репозиторію до `.ai/`. llms.txt залишається в корені (вимога стандарту llmstxt.org).
Зафіксувати рішення в ADR-0004. Оновити всі посилання та CI.

## Goals

- [x] Переміщити STATUS.md → `.ai/STATUS.md`
- [x] Переміщити ROADMAP.md → `.ai/ROADMAP.md`
- [x] Переміщити QUICKSTART.md → `.ai/QUICKSTART.md`
- [x] Переміщити VERSION → `.ai/VERSION`
- [x] `llms.txt` залишити в корені, оновити посилання всередині
- [x] Оновити README.md: дерево директорій та посилання
- [x] Оновити CI `lint.yml`: `VERSION_FILE=".ai/VERSION"`
- [x] Оновити `create-repo-prompt.md`: правильна структура
- [x] Оновити `runbook.uk.md`: посилання на `llms.txt`
- [x] Оновити `project-state.yaml`: SCALE-005 work item, version 5
- [x] Створити ADR-0004: рішення про консолідацію кореневих файлів
- [x] Оновити CHANGELOG.md (Unreleased секція)
- [x] Виправити review-коментарі (посилання, CODEOWNERS, CI yaml-validation)

## What was done

- [x] STATUS.md, ROADMAP.md, QUICKSTART.md, VERSION переміщено до `.ai/`
- [x] llms.txt залишено в корені; посилання всередині оновлено
- [x] README.md: дерево директорій, посилання — оновлено
- [x] `.github/workflows/lint.yml`: `VERSION_FILE=".ai/VERSION"`; project-state перевірка
  тепер використовує `python3 yaml.safe_load()` для перевірки `state.phase`
- [x] `.github/CODEOWNERS`: consolidated to `/.ai/ @dmageyev`
- [x] `create-repo-prompt.md`: структура відповідає реальному репо
- [x] ADR-0004 створено: [`.ai/memory/decisions/0004-root-files-consolidation.md`](../../../memory/decisions/0004-root-files-consolidation.md)
- [x] CHANGELOG.md: Unreleased секція оновлена
- [x] Всі посилання у `.md` перетворено на клікабельні
- [x] `researcher.md`: "дурабельні" → "довготривалі"
- [x] `CONTRIBUTING.md`: `snake_case` → `kebab-case` для YAML
- [x] `.gitignore`: додано `.env`, `*.key`, `*.pem`
- [x] `orchestrator.system.md`: edge case про `project-state.yaml` — не копіювати snapshot-шаблон

## Key decisions

- [ADR-0004](../../../memory/decisions/0004-root-files-consolidation.md): файли шаблону
  переміщено до `.ai/`; `llms.txt` залишається в корені за стандартом llmstxt.org.

## Current state

- **Snapshot:** [`.ai/logs/sessions/2026-05-05-0231-scale-005/snapshot.yaml`](snapshot.yaml)
- **Phase:** `review`
- **Progress:** 90%
- **Open questions:** немає
- **Blockers:** немає
- **PR #1 статус:** відкрито — очікує рев'ю та merge

## Next actions (ordered)

1. Провести рев'ю PR #1 та злити в `main`
2. Оновити `project-state.yaml`: phase → `done`, progress → 100
3. Визначити наступний SCALE work item або перейти до нового milestone

## Files changed / created

- `.ai/STATUS.md` (переміщено з кореня)
- `.ai/ROADMAP.md` (переміщено з кореня)
- `.ai/QUICKSTART.md` (переміщено з кореня)
- `.ai/VERSION` (переміщено з кореня)
- `.ai/memory/decisions/0004-root-files-consolidation.md` (новий ADR)
- `.ai/memory/state/project-state.yaml` (оновлено: version 5, SCALE-005)
- `README.md`, `CHANGELOG.md`, `CONTRIBUTING.md`, `SECURITY.md`, `.gitignore`
- `.github/workflows/lint.yml`, `.github/CODEOWNERS`
- `.ai/docs/bootstrap/create-repo-prompt.md`
- `.ai/workflows/runbook.uk.md`
- `.ai/prompts/system/agent.orchestrator.system.md`
- `.ai/agents/roles/researcher.md`
- `.ai/logs/sessions/README.md`
- `.ai/logs/sessions/2026-05-05-0231-scale-005/snapshot.yaml` (цей файл)
- `.ai/logs/sessions/2026-05-05-0231-scale-005/handoff.md` (цей файл)
