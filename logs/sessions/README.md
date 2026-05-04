# Журнал сесій (Sessions Log)

Ця папка містить **Handoff Packages** — набори артефактів передачі контексту між сесіями.

## Формат

Кожна сесія зберігається у підпапці з іменем у форматі `YYYY-MM-DD-topic`:

```text
logs/sessions/
  YYYY-MM-DD-topic/
    snapshot.yaml   ← машинозчитуваний стан (YAML)
    handoff.md      ← людиночитаний підсумок (Markdown)
    [artifact-*.md] ← опціональні додаткові артефакти
```

## Шаблони

- `prompts/handoff/snapshot.template.yaml`
- `prompts/handoff/handoff.template.md`

## Правила

- Одна папка = одна сесія.
- Нова сесія = нова папка (навіть якщо topic той самий, але дата інша).
- Поле `version` у snapshot.yaml інкрементується в межах одного topic.
- Не видаляй старі сесії — вони є частиною інституційної пам'яті.

## Протокол handoff

Детальний опис: [`docs/03-handoff-protocol.md`](../../docs/03-handoff-protocol.md)
