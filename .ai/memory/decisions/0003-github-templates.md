# ADR-0003: GitHub-шаблони та CODEOWNERS

## Status

`accepted`

## Date

2026-05-04

## Context

Репозиторій є публічним шаблоном. Відсутність стандартних GitHub-шаблонів (issue, PR)
та файлу CODEOWNERS ускладнює внески від спільноти та знижує якість review.

## Decision

Додати до репозиторію:

1. [`.github/ISSUE_TEMPLATE/`](../../../.github/ISSUE_TEMPLATE/) з двома шаблонами:
   - `bug_report.md` — звіт про помилку у шаблоні.
   - `improvement.md` — пропозиція покращення workflow.
2. [`.github/pull_request_template.md`](../../../.github/pull_request_template.md) — стандартний чекліст для PR:
   - Тип зміни (docs / workflow / agent prompt / CI).
   - Чекліст якості: lint проходить, handoff оформлено, ADR додано (якщо потрібно).
3. [`.github/CODEOWNERS`](../../../.github/CODEOWNERS) — визначає `@dmageyev` власником усіх файлів `.ai/`.

## Consequences

- Нові issues автоматично отримують структурований опис.
- PR-автори бачать чекліст якості ще до відкриття PR.
- CODEOWNERS забезпечує обов'язковий review від власника при змінах у `.ai/`.
- Ці файли мають бути включені у `create-repo-prompt.md` для відтворення у нових репозиторіях.
