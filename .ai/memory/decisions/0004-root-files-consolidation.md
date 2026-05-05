# ADR-0004: Консолідація кореневих файлів шаблону до `.ai/`

## Status

`accepted`

## Date

2026-05-05

## Context

При використанні `AI-Workflow` як шаблону для нового проєкту — команда форкає репо
і починає додавати власні файли до кореня. Файли шаблону (`STATUS.md`, `ROADMAP.md`,
`QUICKSTART.md`, `VERSION`, `llms.txt`) залишалися в корені та **змішувалися з файлами
проєкту**, що ускладнювало роботу AI-агентів:

- Агент не міг легко відрізнити "файли AI-Workflow" від "файлів проєкту".
- `ls` / file tree у корені повертав забагато нерелевантних артефактів.
- Підвищувалася когнітивне навантаження при onboarding нового агента.

**Обмеження:**

- `README.md`, `CONTRIBUTING.md`, `CHANGELOG.md`, `SECURITY.md`, `.gitignore`,
  `.github/`, `.markdownlint.json`, `.yamllint.yml` мають залишатися в корені —
  це стандарти GitHub та інструментів лінтингу.

## Decision

Перемістити всі файли, специфічні для AI-Workflow-шаблону, з кореня до `.ai/`:

| Було | Стало |
|------|-------|
| `STATUS.md` | `.ai/STATUS.md` |
| `ROADMAP.md` | `.ai/ROADMAP.md` |
| `QUICKSTART.md` | `.ai/QUICKSTART.md` |
| `VERSION` | `.ai/VERSION` |

**У корені залишаються:**
`README.md`, `llms.txt` (вимога стандарту [llmstxt.org](https://llmstxt.org)),
`CONTRIBUTING.md`, `CHANGELOG.md`, `SECURITY.md`,
`.gitignore`, `.markdownlint.json`, `.yamllint.yml`, `.github/`

## Consequences

- Корінь репо містить мінімум файлів — AI-агент одразу бачить лише `README.md` та
  стандартні метафайли. Всі AI-workflow артефакти ізольовані в `.ai/`.
- `README.md` залишається входом: посилається на `.ai/QUICKSTART.md`, `.ai/STATUS.md`,
  `.ai/ROADMAP.md` тощо.
- CI (`version-changelog-sync`) оновлено: `VERSION_FILE=".ai/VERSION"`.
- Усі внутрішні посилання у переміщених файлах оновлено відповідно до нових шляхів.
- `create-repo-prompt.md` та `runbook.uk.md` оновлено.
